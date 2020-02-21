# h264_qdct_ptc 2020-2-20 

In the 1.2.20 version, we provide the practical H.264 video embedding and extraction tools, and associate codes for explaining PTC in practice. 
 
If you have any question, no hesitate to contact the author.
Author: Yu Wang. Email: wangyu9078@iie.ac.cn

(The project with full source codes will be posted upon the publication of our research).

# Publication
Minimizing Embedding Impact for H.264 Steganography by Progressive Trellis Coding
[Not be published]

# Files Explanation
--embed.bat: contains a case of command line parameters, and double click it to run the embedding tool.

--extract.bat: contains a case of command line parameters, and double click it to run the extraction tool.

--video-decode.bat: contains a case of command line parameters, and double click it to run the H.264 decoder.

--PTC-s.exe: the embedding/encoding tool.

--ext-PTC.exe: the extraction/decoding tool.

--ldecode.exe: an ordinary H.264 decoder.

--meg.txt: a secret message file used for testing the tools. Users can 
modify messages inside arbitrarily.

--walk_cif_cover.264: This is a H.264 video for test, 376 frames, 30 fps, qp=28,  baseline, GOP=10, 352x288.

# quick overview of usage:
For embedding, first of all, we should decode 'walk_cif_cover.264' into raw YUV data file 'walk_cif_cover.yuv'. Next, compress it into a H.264 video stream 'walk_cif_stego.264' while embedding the 'meg.txt' using PTC-s.exe. 
For extraction, We decode the 'walk_cif_stego.264' into a YUV data file while extracting the messages into the file 'ext-meg.txt'.

=========================================

# 1.Compilation
# 2.Code explanation
# 3.command line parameters
# 4.Input/Output file format
# 5.Platform

========================================

# 1.Compilation
Windows
MS Visual C++ 2013 or later

=====================================================================

# 2.Code explanation
(waiting for updates recently)

=====================================================================

# 3.command line parameters
3.1 Encoder/Embedding
Test case:
ptc-s.exe --fps 30 --profile baseline --level 3.0 --threads 1 --qp 28 --keyint 10 --input-res 352x288 --tune psnr --psnr --ssim --megfile meg.txt --tempfile 2temp.txt --seq 18 --pl 3 --embytes 0 -o walk_cif.264 walk_cif.yuv 

--fps frame per second
--qp quantization parameter
--keyint Gop size
--input-res width x height (resolution)
--megfile secret message file
--tempfile temp file
-o stegovideo (.264) covervideo (.yuv) 

3.2 Decoder/Extraction
Test case:
ldecod.exe -p InputFile=walk_cif.264 -p OutputFile=walk_dec.yuv -M ext-message.txt -T messagetemp.txt
-p InputFile=stego video 
-p OutputFile=decoded video
-M messages retrieved
-T temp file

=====================================================================

# 4.Input/Output file format
For message embedding tool:
The source video material is read from raw YUV 4:2:0 data files.
The output is an h.264 video stream.

For message extraction tool:
The source video material is an h.264 video stream.
The output is raw YUV 4:2:0 data files..

=====================================================================

# 5.Platform
(waiting for updates recently)





