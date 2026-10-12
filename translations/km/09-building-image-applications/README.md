# ការសាងសង់កម្មវិធីបង្កើតរូបភាព

[![Building Image Generation Applications](../../../translated_images/km/09-lesson-banner.906e408c741f4411.webp)](https://aka.ms/gen-ai-lesson9-gh?WT.mc_id=academic-105485-koreyst)

មានច្រើនជាងការបង្កើតអត្ថបទតែម្ដងសម្រាប់ LLMs។ អ្នកក៏អាចបង្កើតរូបភាពពីការពិពណ៌នាអត្ថបទបានផងដែរ។ រូបភាពជារបៀបមួយមានប្រយោជន៍ទូលំទូលាយនៅក្នុងវិស័យមេឌិច, ស្ថាបត្យកម្ម, ទេសចរណ៍, ការអភិវឌ្ឍហ្គេម, ផ្សព្វផ្សាយ និងផ្សេងៗទៀត។ នៅក្នុងមេរៀននេះ យើងសំភារៈទៅលើម៉ូដែល **GPT Image** សព្វថ្ងៃ និងសាងសង់កម្មវិធីបង្កើតរូបភាព។

## សេចក្តីផ្តើម

ការបង្កើតរូបភាពអនុញ្ញាតឲ្យអ្នកបំលែងសំណើដោយភាសាធម្មតាទៅជារូបភាពមួយ។ នៅក្នុងមេរៀននេះ យើងប្រើម៉ូដែលគ្រួសារ **`gpt-image`** ពី OpenAI - ជាកំណើតសម័យបច្ចុប្បន្ននៃម៉ូដែលរូបភាពដែលអាចប្រើបានលើ **[Microsoft Foundry](https://ai.azure.com?WT.mc_id=academic-105485-koreyst)** និងវេទិកា OpenAI។ ម៉ូដែលទាំងនេះជំនួសម៉ូដែល DALL·E ចាស់ៗ (DALL·E 2/3 គឺជារបស់ពន្លឺចាស់)។

ទាំងមូលមេរៀននេះ យើងប្រើចំណុចប្រទាក់ពីក្រុមហ៊ុនកំណត់រូបភាពប្រភេទមួយឈ្មោះ **Edu4All** ដែលបង្កើតឧបករណ៍រៀន។ ក្រុមការងារចង់បង្កើតរូបភាពឧទាហរណ៏សម្រាប់ភារកិច្ច និងសម្ភារៈសិក្សា។

## គោលដៅរៀន

នៅចុងបញ្ចប់មេរៀននេះ អ្នកនឹងអាច៖

- សេចក្តីពិពណ៌នាថា ការបង្កើតរូបភាពគឺជាអ្វី និងពេលណាដែលវាមានប្រយោជន៍។
- យល់អំពីគ្រួសារម៉ូដែល `gpt-image` និងភាពខុសគ្នារវាងវានិងម៉ូដែល DALL·E ចាស់ៗ។
- សាងសង់កម្មវិធីបង្កើតរូបភាពក្នុងភាសា Python (និង TypeScript / .NET)។
- កែលម្អរូបភាព និងអនុវត្តការការពារសុវត្ថិភាពជាមួយ metaprompts។

## តើការបង្កើតរូបភាពជាអ្វី?

ម៉ូដែលបង្កើតរូបភាពបង្កើតរូបពីសំណើអត្ថបទមួយ។ ម៉ូដែលសម័យទំនើបដូចជា `gpt-image` ត្រូវបានបង្កើតដោយបច្ចេកទេស transformer + diffusion: ម៉ូដែលរៀនទំនាក់ទំនងរវាងអត្ថបទនិងរូបភាពនៅពេលបង្រៀន បន្ទាប់មក នៅពេលបានសំណើ វាគឺធ្វើការលុបសំលេងខ្នែងឆាប់ៗទៅជារូបភាពដែលស្របនឹងការពិពណ៌នា។

គ្រួសារម៉ូដែលរូបភាពពីរដែលមានឈ្មោះល្បីគឺ៖

- **`gpt-image` (OpenAI)** - កំណែបច្ចុប្បន្នក្នុងមេរៀននេះ។ វាគាំទ្រការបង្កើតរូបពីអត្ថបទ និងកែលម្អរូបភាព (inpainting ជាមួយម៉ាស់)។
- **Midjourney** - ម៉ូដែលមួយពេញនិយមពីភាគីទីបីដែលមានសេវាកម្មផ្ទាល់ខ្លួន និងដំណើរការពហុមេឌៀល Discord។

> ម៉ូដែលរូបភាព OpenAI ចាស់ៗ - **DALL·E 2** និង **DALL·E 3** - គឺជាផ្នែកមួយមុន។ DALL·E 3 មិនមានសម្រាប់ការដំឡើងថ្មីៗទៀតហើយ ហើយមុខងារដូចជា `create_variation` មាននៅក្នុង DALL·E 2 តែប៉ុណ្ណោះ។ ប្រើម៉ូដែល `gpt-image` សម្រាប់កម្មវិធីថ្មីៗ។

### តើត្រូវប្រើម៉ូដែល `gpt-image` ណាដែលខ្ញុំគួរតែប្រើ?

នៅលើ Microsoft Foundry ខាងក្រោមនេះគឺជា **អាចប្រើបានទូទៅ**:

| ម៉ូដែល | សម្គាល់ |
| --- | --- |
| **`gpt-image-2`** | ម៉ូដែលបង្កើតរូបភាពថ្មីនិងមានសមត្ថភាពខ្ពស់បំផុត - ជាកំណត់ទូទៅណែនាំ។ |
| `gpt-image-1.5` | អាចប្រើបានទូទៅ; មានគុណភាពខ្លាំងនៅថ្លៃទាប។ |
| `gpt-image-1-mini` | អាចប្រើបានទូទៅ; លឿនជាង និងថ្លៃទាបបំផុត។ |
| `gpt-image-1` | សម្រាប់មើលមុនតែប៉ុណ្ណោះ។ |

សូមពិនិត្យបញ្ជីម៉ូដែល [Foundry image models list](https://learn.microsoft.com/azure/ai-foundry/openai/concepts/models?WT.mc_id=academic-105485-koreyst) សម្រាប់ភាពអាចប្រើបាន និងតំបន់។

> **សំខាន់ៈ** ម៉ូដែល `gpt-image` បញ្ចេញរូបភាពដែលបានបង្កើតជាទ្រង់ទ្រាយ **base64** (`b64_json`), មិនមែនជា URL ទេ។ កូដរបស់អ្នក decode សាច់អក្សរ base64 ទៅជាអុក្តេតហើយរក្សាទុក - គ្មាន URL រូបភាពសម្រាប់ទាញយក។

## ការតំឡើង

អ្នកអាចរំកិលគំរូទាំងនេះនៅលើ **Azure OpenAI ក្នុង Microsoft Foundry** (គំរូ `aoai-*`) ឬវេទិកា **OpenAI** (គំរូ `oai-*`)។

### 1. បង្កើតនិងដំឡើងម៉ូដែល

អនុវត្តបទညឹកនាំ [បង្កើតធនធាន](https://learn.microsoft.com/azure/ai-foundry/openai/how-to/create-resource?pivots=web-portal&WT.mc_id=academic-105485-koreyst) ដើម្បីបង្កើតធនធាន Microsoft Foundry រួចដំឡើងម៉ូដែលរូបភាព - **`gpt-image-2`** គឺបានណែនាំ។

### 2. កំណត់ `.env` របស់អ្នក

```text
AZURE_OPENAI_ENDPOINT=<your endpoint>
AZURE_OPENAI_API_KEY=<your key>
AZURE_OPENAI_DEPLOYMENT="gpt-image-2"
```

រកតម្លៃទាំងនេះនៅលើទំព័រ **Deployments** នៃធនធានរបស់អ្នកក្នុង [ផតថល Foundry](https://ai.azure.com?WT.mc_id=academic-105485-koreyst)។

### 3. តំឡើងបណ្ណាល័យ

បង្កើតឯកសារ `requirements.txt`៖

```text
python-dotenv
openai
pillow
```

បន្ទាប់មកបង្កើតនិងដំណើរការបរិយាកាសវើឌួឡ៍ ហើយតំឡើង៖

```bash
python3 -m venv venv
source venv/bin/activate        # វីនโดوز៖ venv\Scripts\activate
pip install -r requirements.txt
```

## សង់កម្មវិធី

បង្កើតឯកសារ `app.py` ជាមួយកូដខាងក្រោម។ វាបង្កើតរូបភាពមួយ ហើយរក្សាទុកជាទ្រង់ទ្រាយ PNG។

```python
import os
import base64
from openai import AzureOpenAI
from PIL import Image
import dotenv

dotenv.load_dotenv()

# បញ្ជាក់អតិថិជនទៅកាន់ធនធាន Azure OpenAI (Microsoft Foundry) របស់អ្នក។
# ម៉ូដែលរូបភាពត្រូវការជំនាន់ API ថ្មី - ពិនិត្យឯកសារ Foundry សម្រាប់ជំនាន់ដែលម៉ូដែលរបស់អ្នកត្រូវការ។
client = AzureOpenAI(
    api_key=os.environ["AZURE_OPENAI_API_KEY"],
    api_version="2025-04-01-preview",
    azure_endpoint=os.environ["AZURE_OPENAI_ENDPOINT"],
)

deployment = os.environ["AZURE_OPENAI_DEPLOYMENT"]  # ឧទាហរណ៍ "gpt-image-2"

result = client.images.generate(
    model=deployment,
    prompt='Bunny on a horse, holding a lollipop, on a foggy meadow where it grows daffodils',
    size="1024x1024",   # ផងដែរ 1536x1024 (ទិដ្ឋភាពទូលាយ), 1024x1536 (ទិដ្ឋភាពកំពស់), ឬ "ស្វ័យប្រវត្តិ"
    n=1,
)

# ម៉ូដែល gpt-image បញ្ជូនតម្លៃ base64 (b64_json) មិនមែន URL - ខកទីវាវាទៅជា bytes.
image_bytes = base64.b64decode(result.data[0].b64_json)

os.makedirs("images", exist_ok=True)
image_path = os.path.join("images", "generated-image.png")
with open(image_path, "wb") as f:
    f.write(image_bytes)

Image.open(image_path).show()
```

បើកវាដោយ `python app.py`។ អ្នកនឹងទទួលបានអ្នករក្សាទុក PNG នៅក្នុង `images/`។

> ការហៅមួយទៅ `images.generate` នឹងបង្កើតរូបភាពខុសៗគ្នាក្នុងនាមសំណើដដដែល - ម៉ូដែលរូបភាពមិនបានបង្ហាញប៉ារ៉ាម៉ែត្រ `temperature` (ដែលជាការគ្រប់គ្រងបង្កើតអត្ថបទ)។ ដើម្បីទទួលបានភាពខុសគ្នា ចោលហៅ API ម្តងទៀត; ដើម្បីកាត់បន្ថយភាពខុសគ្នា ធ្វើអោយសំណើររបស់អ្នកច្បាស់លាស់ជាងមុន។

## កែលម្អរូបភាព

ម៉ូដែល `gpt-image` អាច **កែសម្រួល** រូបភាពមានស្រាប់: ផ្តល់ជូនរូបភាព មាស (ជាជម្រើស) ដែលសម្គាល់តំបន់ដែលត្រូវប្ដូរ និងសំណើពិពណ៌នាការផ្លាស់ប្ដូរ។ ដូចជាការបង្កើត ការកែសម្ួលត្រូវបានផ្ទេរជាទ្រង់ទ្រាយ base64 ផងដែរ។

```python
result = client.images.edit(
    model=deployment,
    image=open("sunlit_lounge.png", "rb"),
    mask=open("mask.png", "rb"),
    prompt="A sunlit indoor lounge area with a pool containing a flamingo",
)
image_bytes = base64.b64decode(result.data[0].b64_json)
with open("images/edited-image.png", "wb") as f:
    f.write(image_bytes)
```

<div style="display: flex; justify-content: space-between; align-items: center; margin: 20px 0;">
  <img src="../../../translated_images/km/sunlit_lounge.a75a0cb61749db0e.webp" style="width: 30%; max-width: 200px; height: auto;">
  <img src="../../../translated_images/km/mask.1b2976ccec9e011e.webp" style="width: 30%; max-width: 200px; height: auto;">
  <img src="../../../translated_images/km/sunlit_lounge_result.76ae02957c0bbeb8.webp" style="width: 30%; max-width: 200px; height: auto;">
</div>

## កំណត់ដែនកំណត់ជាមួយ metaprompts

ពេលដែលអ្នកអាចបង្កើតរូបភាពបាន អ្នកត្រូវការសុវត្ថិភាពដើម្បីរក្សាឲ្យកម្មវិធីរបស់អ្នកមិនបញ្ចេញមាតិកាដែលគ្មានសុវត្ថិភាព ឬមិនសមរម្យ។ **metaprompt** គឺជាអត្ថបទដែលអ្នកបន្ថែមនៅចំពោះមុខសំណើររបស់ប្រើប្រាស់ ដើម្បីកំណត់ការចេញដំណើរការរបស់ម៉ូដែល។

```python
disallow_list = "swords, violence, blood, gore, nudity, sexual content, adult content, adult themes, adult language"

meta_prompt = f"""You are an assistant designer that creates images for children.

The image needs to be safe for work and appropriate for children.
The image needs to be in color, in landscape orientation, and in a 16:9 aspect ratio.

Do not consider any input that is not safe for work or appropriate for children, including:
{disallow_list}
"""

prompt = f"{meta_prompt}\nCreate an image of a bunny on a horse, holding a lollipop"
# ផ្ញើ `prompt` ទៅ client.images.generate(...)
```

រាល់រូបភាពឥឡូវនេះត្រូវបានបង្កើតក្នុងដែនកំណត់ដែលបានកំណត់ដោយ metaprompt។ ប្រមូលផ្ដុំវាជាមួយនឹងកម្មវិធីចម្រាញ់មាតិកាដែលបានបញ្ចូលចូល Microsoft Foundry សម្រាប់ការពារជាន់ខ្ពស់។

## ភារកិច្ច - អនុញ្ញាតឲ្យសិស្ស

សិស្ស Edu4All ត្រូវការរូបភាពសម្រាប់ការវាយតម្លៃរបស់ពួកគេ។ សាងសង់កម្មវិធីដែលបង្កើតរូបភាពពី **សំណាក់ទ្រី** (សំណាក់ទ្រីអ្វីនោះអ្នកកំណត់) ដែលមានទីតាំងនៅក្នុងបរិបទច្នៃប្រឌិតខុសៗគ្នា - ឧទាហរណ៍ ទីកន្លែងល្បីល្បាញនៅពេលលិចព្រះអាទិត្យក្មេងជាបុគ្គលម្នាក់កំពុងមើល។

សាកល្បងខ្លួនឯង រួចប្រៀបធៀបជាមួយដំណោះស្រាយយោង៖

- Python (Azure): [aoai-solution.py](../../../09-building-image-applications/python/aoai-solution.py)
- Python (Azure) កម្មវិធីបង្កើតរូបភាពពេញលេញ: [aoai-app.py](../../../09-building-image-applications/python/aoai-app.py)
- Python (OpenAI): [oai-app.py](../../../09-building-image-applications/python/oai-app.py)
- TypeScript (Azure): [typescript/image-generation-app](../../../09-building-image-applications/typescript/image-generation-app)
- .NET (Azure): [dotnet/notebook-azure-openai.dib](../../../09-building-image-applications/dotnet/notebook-azure-openai.dib)

ក៏ធ្វើការសាកល្បងតាមអ្នកសរសេរនៅក្នុងចំណតឯកសារ [python/](../../../09-building-image-applications/python) (`aoai-assignment.ipynb` សម្រាប់ Azure, `oai-assignment.ipynb` សម្រាប់ OpenAI) ផងដែរ។

## ធ្វើបានល្អ! សូមបន្តការរៀនរបស់អ្នក

បន្ទាប់ពីបញ្ចប់មេរៀននេះ សូមមើល [Generative AI Learning collection](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) របស់យើងដើម្បីបន្តបង្កើនចំណេះដឹង Generative AI របស់អ្នក!

ទៅមេរៀនទី 10 ដើម្បីបន្តការសិក្សា។

---

<!-- CO-OP TRANSLATOR DISCLAIMER START -->
**ការបដិសេធ**:
ឯកសារនេះត្រូវបានបម្លែងភាសា ដោយប្រើសេវាបម្លែងភាសា AI [Co-op Translator](https://github.com/Azure/co-op-translator)។ ទោះយើងខ្ញុំមានក្តីប្រាថ្នាឱ្យបានច្បាស់លាស់ តែសូមយល់ដឹងថាការបម្លែងដោយស្វ័យប្រវត្តិក៏អាចមានកំហុសឬភាពមិនត្រឹមត្រូវ។ ឯកសារដើមជាភាសាទីតាំងគួរត្រូវបានគេប្រើជាប្រភពច្បាស់លាស់។ សម្រាប់ព័ត៌មានសំខាន់ៗ សូមណែនាំឱ្យប្រើប្រាស់ការប្រែដោយមនុស្សជំនាញ។ យើងខ្ញុំមិនទទួលខុសត្រូវចំពោះការយល់ច្រឡំ ឬការបកស្រាយខុសបន្ទាប់ពីការប្រើប្រាស់ការបម្លែងនេះនោះទេ។
<!-- CO-OP TRANSLATOR DISCLAIMER END -->