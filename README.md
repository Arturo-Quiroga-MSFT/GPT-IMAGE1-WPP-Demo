# GPT-Image-1 Demo Repository

A comprehensive demonstration repository showcasing the capabilities of OpenAI's GPT-Image-1 model on Azure AI Foundry for enterprise image generation use cases.

## 👤 Author

**Arturo Quiroga**  
*Senior Azure AI Partner Solutions Architect*  
*Enterprise Partner Solutions - Microsoft America*

## 🎯 Purpose

This repository demonstrates GPT-Image-1 capabilities for [WPP](https://www.wpp.com/en-ca), showcasing enterprise-grade image generation, editing, and transformation workflows using Azure AI Foundry.

## 🚀 Features

This repository includes comprehensive Jupyter notebooks demonstrating:

### 1. **Image Generation** (`Image generation.ipynb`)
- Text-to-image generation from prompts
- High-quality image synthesis
- Transparent background generation
- Custom sizing options (1024x1024, 1536x1024, 1024x1536)

### 2. **Image Editing** (`Image edition.ipynb`)
- Prompt-based image modifications
- Selective element editing (colors, objects, textures)
- Multiple variation generation
- Real-world editing examples

### 3. **Image Composition** (`Image Compose.ipynb`)
- Multi-image composition
- Fashion and product showcase combinations
- Scene creation from multiple source images
- Brand and product placement scenarios

### 4. **Image Inpainting** (`Image Inpainting.ipynb`)
- Background removal and replacement
- Object modification with masks
- Scene transformation
- Transparent background workflows

### 5. **Image-to-Image Transformation** (`Image to Image.ipynb`)
- **Style Transfer**: Photo to watercolor, oil painting, anime, cartoon
- **Mood & Atmosphere**: Day to night, sunny to rainy, golden hour effects
- **Seasonal Transformations**: Summer to winter, autumn effects
- **Artistic Filters**: Cyberpunk, vintage, fantasy styles
- **Batch Processing**: Apply transformations to multiple images

### 6. **Interactive Web Application** (`streamlitwebapp.ipynb`)
- User-friendly Streamlit interface
- All capabilities in one app
- Real-time image processing
- Download and preview results

## 📋 Prerequisites

- Python 3.8+
- Azure subscription with Azure AI Foundry access
- GPT-Image-1 deployment in Azure AI Foundry
- API key and endpoint credentials

## 🛠️ Installation

1. Clone the repository:
```bash
git clone https://github.com/[your-username]/GPT-IMAGE1.git
cd GPT-IMAGE1
```

2. Create and activate a virtual environment:
```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

3. Install required packages:
```bash
pip install -r requirements.txt
```

4. Configure your Azure credentials:
   - Copy `notebooks/azure.env.template` to `notebooks/azure.env`
   - Update with your Azure AI Foundry credentials:
     ```
     IMAGEGEN_AOAI_RESOURCE=https://your-endpoint.openai.azure.com/
     IMAGEGEN_DEPLOYMENT=gpt-image-1
     IMAGEGEN_AOAI_API_KEY=your-api-key-here
     ```

## 📁 Repository Structure

```
GPT-IMAGE1/
├── notebooks/
│   ├── Image generation.ipynb
│   ├── Image edition.ipynb
│   ├── Image Compose.ipynb
│   ├── Image Inpainting.ipynb
│   ├── Image to Image.ipynb
│   ├── streamlitwebapp.ipynb
│   ├── azure.env (your credentials - not committed)
│   └── images/ (sample images)
├── requirements.txt
├── .gitignore
└── README.md
```

## 🎨 Use Cases for WPP

### Creative & Advertising
- **Ad Campaign Generation**: Create multiple ad variations from text descriptions
- **Product Visualization**: Generate product shots in different settings
- **Brand Asset Creation**: Create consistent branded imagery at scale
- **Concept Visualization**: Transform rough sketches into polished concepts

### Marketing & Content
- **Social Media Content**: Generate platform-optimized images
- **Seasonal Campaigns**: Transform existing assets for different seasons
- **A/B Testing Assets**: Create multiple variations for testing
- **Localized Content**: Adapt imagery for different markets

### Design & Production
- **Mood Boarding**: Generate style references and mood boards
- **Style Transfer**: Apply brand styles to stock photography
- **Background Replacement**: Update product backgrounds efficiently
- **Asset Variations**: Create diverse versions of hero images

## 💡 Key Benefits

- **Speed**: Generate production-ready images in seconds
- **Cost-Effective**: Reduce photography and design costs
- **Scalability**: Create unlimited variations and iterations
- **Consistency**: Maintain brand guidelines across all assets
- **Flexibility**: Quick adjustments and modifications on demand

## 🔧 Usage Examples

### Generate an Image
```python
from openai import AzureOpenAI

client = AzureOpenAI(
    azure_endpoint=os.getenv("IMAGEGEN_AOAI_RESOURCE"),
    api_key=os.getenv("IMAGEGEN_AOAI_API_KEY"),
    api_version="2025-04-01-preview"
)

result = client.images.generate(
    model="gpt-image-1",
    prompt="A luxury perfume bottle on a marble surface with soft lighting",
    n=1,
    quality="high",
    size="1024x1024"
)
```

### Transform an Image Style
```python
images_list = image_to_image(
    image_file="product.jpg",
    prompt="Transform into a watercolor painting style",
    n=2,
    size="1024x1024",
    quality="high"
)
```

## 🔌 REST API Integration for Image-to-Image

For production integrations, WPP can use the Azure OpenAI REST API directly. Below are examples in both Python and TypeScript.

### Python REST API Example

```python
import os
import requests
import base64
from io import BytesIO
from PIL import Image
from datetime import datetime

def image_to_image(image_file, prompt, n=1, size="1024x1024", quality="high"):
    """
    Transforms an input image based on a text prompt using Azure OpenAI's REST API.
    
    This function enables image-to-image transformations such as:
    - Style transfers (photo to painting, realistic to cartoon, etc.)
    - Mood and atmosphere changes (day to night, sunny to rainy)
    - Artistic effects and filters
    - Seasonal transformations
    - Complete reimagining while preserving composition

    Parameters:
        image_file (str): Path to the source image file.
        prompt (str): Text description guiding the image transformation.
        n (int, optional): Number of transformed images to generate. Defaults to 1.
        size (str, optional): Output image size. Options: "1024x1024", "1536x1024", "1024x1536".
        quality (str, optional): Image quality. Options: "high", "medium", "low".

    Returns:
        list[str]: List of file paths to the saved transformed images.
    """
    try:
        # Configuration
        api_key = os.getenv("IMAGEGEN_AOAI_API_KEY")
        endpoint = os.getenv("IMAGEGEN_AOAI_RESOURCE").rstrip('/')
        deployment = os.getenv("IMAGEGEN_DEPLOYMENT", "gpt-image-1")
        api_version = "2025-04-01-preview"
        
        # Headers
        headers = {"api-key": api_key}
        
        # Construct URL
        url = f"{endpoint}/openai/deployments/{deployment}/images/edits?api-version={api_version}"
        
        # Prepare files and data
        files = {"image": open(image_file, "rb")}
        data = {
            "prompt": prompt,
            "n": n,
            "size": size,
            "quality": quality,
        }

        # Send the request
        response = requests.post(url, headers=headers, files=files, data=data)
        response.raise_for_status()
        
        # Get the results
        images_data = response.json()["data"]
        encoded_images = [img["b64_json"] for img in images_data]

        # Parse and save the generated images
        output_images_list = []
        for encoded_image in encoded_images:
            img = Image.open(BytesIO(base64.b64decode(encoded_image)))
            
            # Save image to file
            timestamp = datetime.now().strftime("%Y%m%d_%H%M%S_%f")[:-3]
            output_file = f"transformed_{timestamp}.jpg"
            img.save(output_file)
            print(f"File saved: {output_file}")
            output_images_list.append(output_file)

        return output_images_list

    except Exception as e:
        print(f"Error generating images: {e}")
        return None

# Usage
results = image_to_image(
    image_file="product.jpg",
    prompt="Transform this product photo into a watercolor painting with soft colors",
    n=2,
    size="1024x1024",
    quality="high"
)
```

### TypeScript/Node.js REST API Example

```typescript
import * as fs from 'fs';
import * as path from 'path';
import fetch from 'node-fetch';
import FormData from 'form-data';

interface ImageTransformOptions {
  imageFile: string;
  prompt: string;
  n?: number;
  size?: '1024x1024' | '1536x1024' | '1024x1536';
  quality?: 'high' | 'medium' | 'low';
}

interface ImageResult {
  b64_json: string;
}

async function imageToImage(options: ImageTransformOptions): Promise<string[]> {
  try {
    const {
      imageFile,
      prompt,
      n = 1,
      size = '1024x1024',
      quality = 'high'
    } = options;

    // Configuration
    const apiKey = process.env.IMAGEGEN_AOAI_API_KEY!;
    const endpoint = process.env.IMAGEGEN_AOAI_RESOURCE!.replace(/\/$/, '');
    const deployment = process.env.IMAGEGEN_DEPLOYMENT || 'gpt-image-1';
    const apiVersion = '2025-04-01-preview';

    // Construct URL
    const url = `${endpoint}/openai/deployments/${deployment}/images/edits?api-version=${apiVersion}`;

    // Prepare form data
    const formData = new FormData();
    formData.append('image', fs.createReadStream(imageFile));
    formData.append('prompt', prompt);
    formData.append('n', n.toString());
    formData.append('size', size);
    formData.append('quality', quality);

    // Send the request
    const response = await fetch(url, {
      method: 'POST',
      headers: {
        'api-key': apiKey,
        ...formData.getHeaders()
      },
      body: formData
    });

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const result = await response.json() as { data: ImageResult[] };
    const outputFiles: string[] = [];

    // Process and save images
    for (const imageData of result.data) {
      const buffer = Buffer.from(imageData.b64_json, 'base64');
      const timestamp = new Date().toISOString().replace(/[:.]/g, '-');
      const outputFile = `transformed_${timestamp}.jpg`;
      
      fs.writeFileSync(outputFile, buffer);
      console.log(`File saved: ${outputFile}`);
      outputFiles.push(outputFile);
    }

    return outputFiles;

  } catch (error) {
    console.error('Error generating images:', error);
    return [];
  }
}

// Usage
(async () => {
  const results = await imageToImage({
    imageFile: 'product.jpg',
    prompt: 'Transform this product photo into a watercolor painting with soft colors',
    n: 2,
    size: '1024x1024',
    quality: 'high'
  });
  
  console.log('Generated images:', results);
})();
```

### REST API Key Points for WPP

1. **Endpoint Structure**: `{endpoint}/openai/deployments/{deployment}/images/edits?api-version={version}`
2. **Authentication**: Use `api-key` header with your Azure OpenAI key
3. **Multipart Form Data**: Send image file and parameters as form data
4. **Response Format**: Base64-encoded images in JSON response
5. **Rate Limits**: Monitor quota and implement retry logic for production
6. **Error Handling**: Always handle network errors and API rate limits gracefully

### Required Dependencies

**Python:**
```bash
pip install requests pillow python-dotenv
```

**TypeScript/Node.js:**
```bash
npm install node-fetch form-data @types/node
```

## 📚 Documentation

- [Azure AI Foundry Documentation](https://learn.microsoft.com/azure/ai-studio/)
- [GPT-Image-1 Announcement](https://azure.microsoft.com/en-us/blog/unveiling-gpt-image-1-rising-to-new-heights-with-image-generation-in-azure-ai-foundry/)
- [OpenAI API Reference](https://platform.openai.com/docs/guides/images)

## 🤝 Contributing

This is a demonstration repository. For questions or suggestions, please contact Arturo Quiroga at Microsoft.

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## ⚠️ Important Notes

- **API Keys**: Never commit your `azure.env` file or expose your API keys
- **Costs**: Azure AI services incur costs - monitor your usage
- **Rate Limits**: Be aware of API rate limits and quotas
- **Content Policy**: All generated content must comply with Azure AI content policies

## 🔗 Additional Resources

- [Azure AI Foundry Portal](https://ai.azure.com/)
- [WPP Official Website](https://www.wpp.com/en-ca)
- [Microsoft AI Solutions](https://www.microsoft.com/ai)

---

**Demo prepared for WPP** | **Powered by Azure AI Foundry** | **GPT-Image-1**
