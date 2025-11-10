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
│   ├── Azure AI Foundry gpt-image-1 - Image generation.ipynb
│   ├── Azure AI Foundry gpt-image-1 - Image edition.ipynb
│   ├── Azure AI Foundry gpt-image-1 - Image Compose.ipynb
│   ├── Azure AI Foundry gpt-image-1 - Image Inpainting.ipynb
│   ├── Azure AI Foundry gpt-image-1 - Image to Image.ipynb
│   ├── Azure AI Foundry gpt-image-1 - streamlitwebapp.ipynb
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
