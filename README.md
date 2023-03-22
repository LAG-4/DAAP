# DAAP

!pip3 install imageio==2.4.1 
!pip install moviepy 
!pip install pytube

from pytube import YouTube
from moviepy.video.io.VideoFileClip import VideoFileClip

# define the list of YouTube video URLs
urls = ['https://www.youtube.com/watch?v=JR0xYosoojg',
        'https://www.youtube.com/watch?v=GEUSXnRulUI',
        'https://www.youtube.com/watch?v=QXraHY1Ofuw',
        'https://www.youtube.com/watch?v=D__-i6DZCNg',
        'https://www.youtube.com/watch?v=yzVImnZ0Ji0',
        'https://www.youtube.com/watch?v=xdR3PG39Wh0',
        'https://www.youtube.com/watch?v=FBrVlMihUZM&t=19s',
        'https://www.youtube.com/watch?v=eV59wXCTy2M',
        'https://www.youtube.com/watch?v=D0uP5nXtF4w',
        'https://www.youtube.com/watch?v=TulXGQydVIo',
        'https://www.youtube.com/watch?v=_t6w7gSUndg',
        'https://www.youtube.com/watch?v=JYtZ2zsdE_s',
        'https://www.youtube.com/watch?v=nZZL8-3dfaI',
        'https://www.youtube.com/watch?v=4ua2CUeOg2k',
        'https://www.youtube.com/watch?v=91NxP19F554',
        'https://www.youtube.com/watch?v=iWOjBQMR9Zg&t=13s',
        'https://www.youtube.com/watch?v=7k0iuW2n2ZI']

# loop through each URL in the list
for i, url in enumerate(urls):
    
    # create a YouTube object
    yt = YouTube(url)

    # get the video stream with 4K resolution
    video_stream = yt.streams.filter(res="2160p").first()

    # create a unique output filename for each video
    output_file_path = f"/content/video{i}.mp4"

    # download the video stream
    video_stream.download(output_path=".", filename=output_file_path)

    # define the input path for the trimmed video
    input_path_file = output_file_path 

    # trim the video from 10 to 20 seconds
    trimmedvideo = VideoFileClip(input_path_file).subclip(10, 20)

    # create a unique output filename for each trimmed video
    output_file_path_trimmed = f"/content/trimmedvideo{i}.mp4"

    # write the trimmed video to file
    trimmedvideo.write_videofile(output_file_path_trimmed)
