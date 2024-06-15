# LlamaParse

###
RAG với file excel cho chatbot
Thách thức với chatbot, tool AI hiện này là khó xử lý các file excel và có số liệu như bảng dưới đây.
Trên nền tảng chatgpt thì openai họ sử dụng python để đọc và xử lý file, trước khi model AI nhảy vào tham gia trả lời dựa trên kết quả do python trả về, nhưng cách này rất phức tạp, cũng dễ xảy ra lỗi, và cũng khó nếu các bạn muốn phát triển chatbot riêng.
Tệp Excel thường có bố cục nội dung trên định dạng lưới - mỗi sheet lại có nhiều bảng rời rạc trên một trang tính, đa phần không được sắp xếp dễ dọc vì mỗi người làm một kiểu bảng tính khác nhau.
Trước đây, nhiều phương pháp làm đứt gãy các bảng tính và khiến chúng chồng lên nhau, gây ra hiện tượng ảo giác ở model AI trong việc hiểu dữ liệu này.
Như các bài chia sẻ trước đây, phương pháp RAG hiện nay vẫn là cách tốt và rẻ tiền nhất để train các dữ liệu cho AI trả lời. 
Và LlamaIndex một đơn vị chuyên tạo RAG cho các chatbot đã cung cấp cách thức rất tốt để đọc, hiểu, embedding các dữ liệu trên file excel.
Follow Đặng Hữu Sơn cập nhật thêm nhiều bài viết về AI
###

LlamaParse is an API created by LlamaIndex to efficiently parse and represent files for efficient retrieval and context augmentation using LlamaIndex frameworks.

LlamaParse directly integrates with [LlamaIndex](https://github.com/run-llama/llama_index).

Free plan is up to 1000 pages a day. Paid plan is free 7k pages per week + 0.3c per additional page.

Read below for some quickstart information, or see the [full documentation](https://docs.cloud.llamaindex.ai/).

## Getting Started

First, login and get an api-key from [**https://cloud.llamaindex.ai ↗**](https://cloud.llamaindex.ai).

Then, make sure you have the latest LlamaIndex version installed.

**NOTE:** If you are upgrading from v0.9.X, we recommend following our [migration guide](https://pretty-sodium-5e0.notion.site/v0-10-0-Migration-Guide-6ede431dcb8841b09ea171e7f133bd77), as well as uninstalling your previous version first.

```
pip uninstall llama-index  # run this if upgrading from v0.9.x or older
pip install -U llama-index --upgrade --no-cache-dir --force-reinstall
```

Lastly, install the package:

`pip install llama-parse`

Now you can run the following to parse your first PDF file:

```python
import nest_asyncio

nest_asyncio.apply()

from llama_parse import LlamaParse

parser = LlamaParse(
    api_key="llx-...",  # can also be set in your env as LLAMA_CLOUD_API_KEY
    result_type="markdown",  # "markdown" and "text" are available
    num_workers=4,  # if multiple files passed, split in `num_workers` API calls
    verbose=True,
    language="en",  # Optionally you can define a language, default=en
)

# sync
documents = parser.load_data("./my_file.pdf")

# sync batch
documents = parser.load_data(["./my_file1.pdf", "./my_file2.pdf"])

# async
documents = await parser.aload_data("./my_file.pdf")

# async batch
documents = await parser.aload_data(["./my_file1.pdf", "./my_file2.pdf"])
```

## Using with `SimpleDirectoryReader`

You can also integrate the parser as the default PDF loader in `SimpleDirectoryReader`:

```python
import nest_asyncio

nest_asyncio.apply()

from llama_parse import LlamaParse
from llama_index.core import SimpleDirectoryReader

parser = LlamaParse(
    api_key="llx-...",  # can also be set in your env as LLAMA_CLOUD_API_KEY
    result_type="markdown",  # "markdown" and "text" are available
    verbose=True,
)

file_extractor = {".pdf": parser}
documents = SimpleDirectoryReader(
    "./data", file_extractor=file_extractor
).load_data()
```

Full documentation for `SimpleDirectoryReader` can be found on the [LlamaIndex Documentation](https://docs.llamaindex.ai/en/stable/module_guides/loading/simpledirectoryreader.html).

## Examples

Several end-to-end indexing examples can be found in the examples folder

- [Getting Started](examples/demo_basic.ipynb)
- [Advanced RAG Example](examples/demo_advanced.ipynb)
- [Raw API Usage](examples/demo_api.ipynb)

## Documentation

[https://docs.cloud.llamaindex.ai/](https://docs.cloud.llamaindex.ai/)

## Terms of Service

See the [Terms of Service Here](./TOS.pdf).
