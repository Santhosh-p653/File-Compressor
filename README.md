
# ⚡ Multi-Threaded Huffman File Compressor & Decompressor

A **high-performance, multithreaded file compression and decompression tool** based on the **Huffman Coding Algorithm** — written entirely in modern C++17.

This project efficiently splits large files into chunks, compresses them in parallel threads, and then reconstructs them — achieving excellent speed and compression ratio.

---

## 🚀 Features

✅ **Multithreaded processing** – Utilizes multiple CPU cores for faster compression/decompression  
✅ **Huffman Coding** – Lossless data compression  
✅ **Chunk-based architecture** – Handles very large files efficiently  
✅ **Cross-platform path handling** – Works seamlessly on Windows, Linux, and macOS  
✅ **Thread-safe queues** – Robust concurrency management  
✅ **Compression statistics** – View compression ratio and processing time  

---

## 🧠 How It Works

### 🔹 Compression Mode (`c`)
1. Input file is read in fixed-size chunks (default 1 MB each).  
2. Each chunk is sent to a worker thread through a thread-safe queue.  
3. Worker compresses the chunk using Huffman coding and sends it back.  
4. Main thread writes compressed data + Huffman code metadata into the output file.

### 🔹 Decompression Mode (`d`)
1. Reads Huffman code metadata for each chunk.  
2. Sends compressed data to multiple worker threads.  
3. Each thread reconstructs original data.  
4. Main thread writes decompressed chunks sequentially.

---

## 🧩 Architecture Overview

```

┌──────────────────────────┐
│        Main Thread       │
├─────────────┬────────────┤
│ Reads file  │ Writes file│
│  in chunks  │  sequentially
└──────┬──────┘
│
▼
┌──────────────┐     ┌──────────────┐
│  SafeQueue   │ --> │  WorkerThread│
│ (inputQueue) │     │ (compression)│
└──────────────┘     └──────────────┘
│
▼
┌──────────────┐
│  SafeQueue   │
│ (outputQueue)│
└──────────────┘

````

---

## ⚙️ Usage

### 🧱 Build

Make sure you’re using a C++17-compatible compiler.

```bash
g++ -std=c++17 -pthread main.cpp -o huffman
````

### ▶️ Run

#### 🔸 Compression

```bash
./huffman
Enter mode (c for compress, d for decompress): c
Enter input file path: input.txt
Enter output file path: output.huf
Enter number of threads (default 4): 4
Enter chunk size in MB (default 1): 1
```

#### 🔸 Decompression

```bash
./huffman
Enter mode (c for compress, d for decompress): d
Enter input file path: input.huf
Enter output file path: output.txt
Enter number of threads (default 4): 4
Enter chunk size in MB (default 1): 1


---

## 📊 Example Output


Starting compression with 4 threads and chunk size 1 MB...
Processing chunk 0 (20% complete)
Processing chunk 1 (40% complete)
...

-------- Operation Statistics --------
Operation: Compression
Input file size: 10,485,760 bytes
Output file size: 3,242,112 bytes
Compression ratio: 69.09%
Processing time: 4.32 seconds
Threads used: 4
Chunk size: 1 MB
----------------------------------

Operation completed successfully! Output file: output.huf

```
---

## 🧮 Huffman Coding Summary

Huffman Coding is a **lossless compression algorithm** that assigns shorter binary codes to more frequent characters and longer codes to less frequent ones.

Example:

| Character | Frequency | Code  |
| --------- | --------- | ----- |
| `a`       | 10        | `0`   |
| `b`       | 5         | `10`  |
| `c`       | 2         | `110` |
| `d`       | 1         | `111` |

Text `"abac"` → binary `"0100110"`

---

## 📁 File Structure


├── main.cpp          # Main source file
├── README.md         # Documentation
└── (output files)
    ├── input.txt
    ├── output.huf
    └── decompressed.txt




## 💡 Key Components

| Component            | Purpose                                          |
| -------------------- | ------------------------------------------------ |
| `normalizePath()`    | Cleans and converts file paths                   |
| `SafeQueue`          | Thread-safe queue for inter-thread communication |
| `HuffmanNode`        | Represents tree node with char and frequency     |
| `buildHuffmanTree()` | Builds Huffman tree from frequency map           |
| `generateCodes()`    | Generates binary codes recursively               |
| `compressChunk()`    | Compresses a single file chunk                   |
| `decompressChunk()`  | Restores original chunk                          |
| `worker()`           | Handles per-thread compression                   |
| `decompressWorker()` | Handles per-thread decompression                 |



## 🧪 Performance Tips

* Use higher thread counts (`NUM_THREADS`) for large files.
* Adjust chunk size (`CHUNK_SIZE`) for optimal CPU utilization.
* SSD storage improves I/O speed.
* Avoid running with too many threads on low-core CPUs.


## 🛠️ Requirements

* C++17 or later
* g++ / clang++ / MSVC
* Supported OS: Windows, Linux, macOS



## 🧾 License

This project is open-source and free to use under the **MIT License**.


## ✨ Author

**Palguna Shetty**
🎓 B.E. in Computer Science & Engineering (2026)
📧 [[palgunashetty263@example.com](mailto:palgunashetty263@example.com)]
🌐 [GitHub Profile](https://github.com/palguna26)



> “Parallelism is not just speed — it’s efficiency done right.”


