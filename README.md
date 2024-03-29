# h264_qdct_ptc 
<b> Timeline </b><br/>

2020-9-3: The source codes are undergoing the security check. After the check, we will upload the missing source codes.

2020-8-20: After the publication, we start to upload the entire source codes since the previous version is not complete.  

From 2020-2-20 to 2020-3-1:
In the 1.2.20 version, we provide the practical H.264 video embedding and extraction tools, and associate (partial) codes for explaining PTC in practice. 
Note that the version is not the final and stable one.
The project with full source codes will be posted upon the publication/accepted of our research, for boosting video steganography.

If you have any question, or find bugs, no hesitate to contact the author.
Author: Yu Wang. Email: ~~wangyu9078@iie.ac.cn~~ (This email has been withdrewed for the author's departure from IIE.)

<b> Publication </b><br/>
Minimizing Embedding Impact for H.264 Steganography by Progressive Trellis Coding
[Not be published]

<b> Quick overview of usage </b><br/>
For embedding, first of all, we should decode 'walk_cif_cover.264' into raw YUV data file 'walk_cif_cover.yuv'. Next, compress it into a H.264 video stream 'walk_cif_stego.264' while embedding the 'meg.txt' using PTC-s.exe. 
For extraction, We decode the 'walk_cif_stego.264' into a YUV data file while extracting the messages into the file 'ext-meg.txt'.

1. double click 'video-decode.bat', to obtain a cover 'walk_cif_cover.yuv'.
2. double click 'embed.bat', to embed 'ext-meg.txt' into 'walk_cif_cover.yuv', and obtain a stego 'walk_cif_stego.264'.
3. double click 'extract.bat', to extract the secret message into 'ext-meg.txt' (a new generated file) from 'walk_cif_stego.264'.
(Note: if users meet runtime erors, like missing .dll, etc, just be free to contact my email.)

<b> Files Explanation </b><br/>

--PTCodes (souce folder): contains all source codes. (Before research pulicaiton/accepted, we only provide a associate/necessary revised .c files, namely encoder_p.c, which includes ptrellis_coding, restore_context, x264_slice_write functions. If you are interested in the frame compression, look into the x264_slice_write function. If you are interested in coding contexts maintained, look into restore_context function. Last but not least, the progressive trellis coding process, that controls multiple coding contexts to expand paths, prune sub-optimal paths, match messages, and retrace short paths, is included in the ptrellis_coding function. 
Note that other necessary steps that dynamically generating multiple cover blocks/stego blocks, the block-by-block coding/modification and the general coder control, etc, are not updated yet.
Besides, more .c and .h files, such as x264.c/.h, macroblock_p.c/.h, common_p.c/.h, ratecontrol_p.c/.h, etc., are revised for the implementation of PTC.
We will continually update this project and tell following video steganographic researchers how to compile the project on window/vs, how to modify the source codes to make steganographic modules integrated into video compression (that is a tough job). 

--embed.bat: contains a case of command line parameters, and double click it to run the embedding tool.

--extract.bat: contains a case of command line parameters, and double click it to run the extraction tool.

--video-decode.bat: contains a case of command line parameters, and double click it to run the H.264 decoder.

--PTC-s.exe: the embedding/encoding tool.

--ext-PTC.exe: the extraction/decoding tool.

--ldecode.exe: an ordinary H.264 decoder.

--meg.txt: a secret message file used for testing the tools. Users can 
modify messages inside arbitrarily.

--walk_cif_cover.264: This is a H.264 video for test, 376 frames, 30 fps, qp=28,  baseline, GOP=10, 352x288.

=========================================

<b> 1.Compilation </b><br/>
<b> 2.Code explanation </b><br/>
<b> 3.command line parameters </b><br/>
<b> 4.Input/Output file format </b><br/>

=========================================

<b> 1.Compilation </b><br/>
Windows
MS Visual C++ 2013 or later
(waiting for updates recently)

<b> 2.Code explanation </b><br/>
(waiting for updates recently)

<b> 3.command line parameters </b><br/>
3.1 Encoder/Embedding
Test case:
ptc-s.exe --fps 30 --profile baseline --level 3.0 --threads 1 --qp 28 --keyint 10 --input-res 352x288 --tune psnr --psnr --ssim --megfile meg.txt --tempfile 2temp.txt --seq 18 --pl 3 --embytes 0 -o walk_cif_stego.264 walk_cif_cover.yuv 

--fps frame per second
--qp quantization parameter
--keyint Gop size
--input-res width x height (resolution)
--megfile secret message file
--tempfile temp file
-o stegovideo (.264) covervideo (.yuv) 

3.2 Decoder/Extraction
Test case:
ext-PTC.exe -p InputFile=walk_cif_stego.264 -p OutputFile=walk_stego_dec.yuv -M ext-meg.txt -T messagetemp.txt
-p InputFile=stego video 
-p OutputFile=decoded video
-M messages retrieved
-T temp file


<b> 4.Input/Output file format </b><br/>
For message embedding tool:
The source video material is read from raw YUV 4:2:0 data files.
The output is an h.264 video stream.

For message extraction tool:
The source video material is an h.264 video stream.
The output is raw YUV 4:2:0 data files.






