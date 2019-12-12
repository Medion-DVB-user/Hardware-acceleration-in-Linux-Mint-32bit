# Hardware-acceleration-in-Linux-Mint-32bit
vpdau fails in vlc and mpv - high cpu consumption

If i play videos (MP4 in H264) with vlc and mpv in Linux Mint Xfce (32bit), vlc displays in terminal glconv_vaapi_x11 gl an error. Vlc seems to play the video with a little more cpu consumption (~ 15%-18%) and mpv takes more cpu usage (25%-35%). vdpauinfo shows that my Radon HD 6670 works fine with vdpau. It is always so in xubunt 18.04 and lubuntu in 32bit version. So it seems to ba a failure in ubuntu 32bit generally.

heinz@heinz-MS-7091:~/Videos/Test-Videos$ ls
'RTL Television_Kung Fu Panda 2 - Doppelt bärenstark_edit.ts'
'WORLD - CRUISE 2010 - 720.mp4'
heinz@heinz-MS-7091:~/Videos/Test-Videos$ vlc 'WORLD - CRUISE 2010 - 720.mp4'
VLC media player 3.0.8 Vetinari (revision 3.0.8-0-gf350b6b5a7)
[01214ba0] main libvlc: VLC wird mit dem Standard-Interface ausgeführt. Benutzen Sie 'cvlc', um VLC ohne Interface zu verwenden.
qt5ct: using qt5ct plugin
qt5ct: D-Bus global menu: no
qt5ct: D-Bus system tray: no
libva info: VA-API version 1.1.0
libva info: va_getDriverName() returns 0
libva info: Trying to open /usr/lib/i386-linux-gnu/dri/r600_drv_video.so
libva info: Found init function __vaDriverInit_1_1
libva info: va_openDriver() returns 0
[9486a9c0] glconv_vaapi_x11 gl error: vaDeriveImage: invalid VASurfaceID
[015313a0] main video output error: video output creation failed
[012c6940] main decoder error: failed to create video output
[012c6940] avcodec decoder: Using G3DVL VDPAU Driver Shared Library version 1.0 for hardware decoding
QObject::~QObject: Timers cannot be stopped from another thread
heinz@heinz-MS-7091:~/Videos/Test-Videos$ 
heinz@heinz-MS-7091:~/Videos/Test-Videos$ 
heinz@heinz-MS-7091:~/Videos/Test-Videos$ mpv 'WORLD - CRUISE 2010 - 720.mp4'
Playing: WORLD - CRUISE 2010 - 720.mp4
 (+) Video --vid=1 (*) (h264 1280x720 29.970fps)
 (+) Audio --aid=1 --alang=und (*) (aac 2ch 44100Hz)
VO does not support requested hardware decoder, or loading it failed.
AO: [pulse] 44100Hz stereo 2ch float
VO: [opengl] 1280x720 yuv420p
AV: 00:00:20 / 00:16:52 (1%) A-V:  0.000


Exiting... (Quit)
heinz@heinz-MS-7091:~/Videos/Test-Videos$ 

vdpauinfo shows:

heinz@heinz-MS-7091:~/Videos/Test-Videos$ vdpauinfo
display: :0.0   screen: 0
API version: 1
Information string: G3DVL VDPAU Driver Shared Library version 1.0

Video surface:

name   width height types
-------------------------------------------
420    16384 16384  NV12 YV12 
422    16384 16384  UYVY YUYV 
444    16384 16384  Y8U8V8A8 V8U8Y8A8 

Decoder capabilities:

name                        level macbs width height
----------------------------------------------------
MPEG1                          --- not supported ---
MPEG2_SIMPLE                    3  9216  2048  1152
MPEG2_MAIN                      3  9216  2048  1152
H264_BASELINE                  41  9216  2048  1152
H264_MAIN                      41  9216  2048  1152
H264_HIGH                      41  9216  2048  1152
VC1_SIMPLE                      1  9216  2048  1152
VC1_MAIN                        2  9216  2048  1152
VC1_ADVANCED                    4  9216  2048  1152
MPEG4_PART2_SP                  3  9216  2048  1152
MPEG4_PART2_ASP                 5  9216  2048  1152
DIVX4_QMOBILE                  --- not supported ---
DIVX4_MOBILE                   --- not supported ---
DIVX4_HOME_THEATER             --- not supported ---
DIVX4_HD_1080P                 --- not supported ---
DIVX5_QMOBILE                  --- not supported ---
DIVX5_MOBILE                   --- not supported ---
DIVX5_HOME_THEATER             --- not supported ---
DIVX5_HD_1080P                 --- not supported ---
H264_CONSTRAINED_BASELINE       0  9216  2048  1152
H264_EXTENDED                  --- not supported ---
H264_PROGRESSIVE_HIGH          --- not supported ---
H264_CONSTRAINED_HIGH          --- not supported ---
H264_HIGH_444_PREDICTIVE       --- not supported ---
HEVC_MAIN                      --- not supported ---
HEVC_MAIN_10                   --- not supported ---
HEVC_MAIN_STILL                --- not supported ---
HEVC_MAIN_12                   --- not supported ---
HEVC_MAIN_444                  --- not supported ---

Output surface:

name              width height nat types
----------------------------------------------------
B8G8R8A8         16384 16384    y  NV12 YV12 UYVY YUYV Y8U8V8A8 V8U8Y8A8 A4I4 I4A4 A8I8 I8A8 
R8G8B8A8         16384 16384    y  NV12 YV12 UYVY YUYV Y8U8V8A8 V8U8Y8A8 A4I4 I4A4 A8I8 I8A8 
R10G10B10A2      16384 16384    y  NV12 YV12 UYVY YUYV Y8U8V8A8 V8U8Y8A8 A4I4 I4A4 A8I8 I8A8 
B10G10R10A2      16384 16384    y  NV12 YV12 UYVY YUYV Y8U8V8A8 V8U8Y8A8 A4I4 I4A4 A8I8 I8A8 

Bitmap surface:

name              width height
------------------------------
B8G8R8A8         16384 16384
R8G8B8A8         16384 16384
R10G10B10A2      16384 16384
B10G10R10A2      16384 16384
A8               16384 16384

Video mixer:

feature name                    sup
------------------------------------
DEINTERLACE_TEMPORAL             y
DEINTERLACE_TEMPORAL_SPATIAL     -
INVERSE_TELECINE                 -
NOISE_REDUCTION                  y
SHARPNESS                        y
LUMA_KEY                         y
HIGH QUALITY SCALING - L1        y
HIGH QUALITY SCALING - L2        -
HIGH QUALITY SCALING - L3        -
HIGH QUALITY SCALING - L4        -
HIGH QUALITY SCALING - L5        -
HIGH QUALITY SCALING - L6        -
HIGH QUALITY SCALING - L7        -
HIGH QUALITY SCALING - L8        -
HIGH QUALITY SCALING - L9        -

parameter name                  sup      min      max
-----------------------------------------------------
VIDEO_SURFACE_WIDTH              y        48     2048
VIDEO_SURFACE_HEIGHT             y        48     1152
CHROMA_TYPE                      y  
LAYERS                           y         0        4

attribute name                  sup      min      max
-----------------------------------------------------
BACKGROUND_COLOR                 y  
CSC_MATRIX                       y  
NOISE_REDUCTION_LEVEL            y      0.00     1.00
SHARPNESS_LEVEL                  y     -1.00     1.00
LUMA_KEY_MIN_LUMA                y  
LUMA_KEY_MAX_LUMA                y  


heinz@heinz-MS-7091:~/Videos/Test-Videos$ 

I hope hardware acceleration becomes fixed in 32bit versions, because my dvb-s2-card for sattelite TV needs about to 50% for watching TV without hardware acceleration. In xubuntu 16.04 it needs only about 10% cpu consumption. Also vlc and mpv needs only 4% to 8% of the cpu powerin xubuntu 16.04!heinz@heinz-MS-7091:~/Videos/Test-Videos$ vdpauinfo
display: :0.0   screen: 0
API version: 1
Information string: G3DVL VDPAU Driver Shared Library version 1.0

Video surface:

name   width height types
-------------------------------------------
420    16384 16384  NV12 YV12 
422    16384 16384  UYVY YUYV 
444    16384 16384  Y8U8V8A8 V8U8Y8A8 

Decoder capabilities:

name                        level macbs width height
----------------------------------------------------
MPEG1                          --- not supported ---
MPEG2_SIMPLE                    3  9216  2048  1152
MPEG2_MAIN                      3  9216  2048  1152
H264_BASELINE                  41  9216  2048  1152
H264_MAIN                      41  9216  2048  1152
H264_HIGH                      41  9216  2048  1152
VC1_SIMPLE                      1  9216  2048  1152
VC1_MAIN                        2  9216  2048  1152
VC1_ADVANCED                    4  9216  2048  1152
MPEG4_PART2_SP                  3  9216  2048  1152
MPEG4_PART2_ASP                 5  9216  2048  1152
DIVX4_QMOBILE                  --- not supported ---
DIVX4_MOBILE                   --- not supported ---
DIVX4_HOME_THEATER             --- not supported ---
DIVX4_HD_1080P                 --- not supported ---
DIVX5_QMOBILE                  --- not supported ---
DIVX5_MOBILE                   --- not supported ---
DIVX5_HOME_THEATER             --- not supported ---
DIVX5_HD_1080P                 --- not supported ---
H264_CONSTRAINED_BASELINE       0  9216  2048  1152
H264_EXTENDED                  --- not supported ---
H264_PROGRESSIVE_HIGH          --- not supported ---
H264_CONSTRAINED_HIGH          --- not supported ---
H264_HIGH_444_PREDICTIVE       --- not supported ---
HEVC_MAIN                      --- not supported ---
HEVC_MAIN_10                   --- not supported ---
HEVC_MAIN_STILL                --- not supported ---
HEVC_MAIN_12                   --- not supported ---
HEVC_MAIN_444                  --- not supported ---

Output surface:

name              width height nat types
----------------------------------------------------
B8G8R8A8         16384 16384    y  NV12 YV12 UYVY YUYV Y8U8V8A8 V8U8Y8A8 A4I4 I4A4 A8I8 I8A8 
R8G8B8A8         16384 16384    y  NV12 YV12 UYVY YUYV Y8U8V8A8 V8U8Y8A8 A4I4 I4A4 A8I8 I8A8 
R10G10B10A2      16384 16384    y  NV12 YV12 UYVY YUYV Y8U8V8A8 V8U8Y8A8 A4I4 I4A4 A8I8 I8A8 
B10G10R10A2      16384 16384    y  NV12 YV12 UYVY YUYV Y8U8V8A8 V8U8Y8A8 A4I4 I4A4 A8I8 I8A8 

Bitmap surface:

name              width height
------------------------------
B8G8R8A8         16384 16384
R8G8B8A8         16384 16384
R10G10B10A2      16384 16384
B10G10R10A2      16384 16384
A8               16384 16384

Video mixer:

feature name                    sup
------------------------------------
DEINTERLACE_TEMPORAL             y
DEINTERLACE_TEMPORAL_SPATIAL     -
INVERSE_TELECINE                 -
NOISE_REDUCTION                  y
SHARPNESS                        y
LUMA_KEY                         y
HIGH QUALITY SCALING - L1        y
HIGH QUALITY SCALING - L2        -
HIGH QUALITY SCALING - L3        -
HIGH QUALITY SCALING - L4        -
HIGH QUALITY SCALING - L5        -
HIGH QUALITY SCALING - L6        -
HIGH QUALITY SCALING - L7        -
HIGH QUALITY SCALING - L8        -
HIGH QUALITY SCALING - L9        -

parameter name                  sup      min      max
-----------------------------------------------------
VIDEO_SURFACE_WIDTH              y        48     2048
VIDEO_SURFACE_HEIGHT             y        48     1152
CHROMA_TYPE                      y  
LAYERS                           y         0        4

attribute name                  sup      min      max
-----------------------------------------------------
BACKGROUND_COLOR                 y  
CSC_MATRIX                       y  
NOISE_REDUCTION_LEVEL            y      0.00     1.00
SHARPNESS_LEVEL                  y     -1.00     1.00
LUMA_KEY_MIN_LUMA                y  
LUMA_KEY_MAX_LUMA                y  


heinz@heinz-MS-7091:~/Videos/Test-Videos$ 




