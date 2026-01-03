# -# 라이브러리 설치
!pip install youtube-comment-downloader

# 동영상 리스트 준비
video_urls = [
    " 동영상 링크"
    
    # 생략: 이하 영상 URL 계속 추가
]

from youtube_comment_downloader import YoutubeCommentDownloader
import pandas as pd

downloader = YoutubeCommentDownloader()
results = []

for url in video_urls:
    video_id = url.split('v=')[-1]
    try:
        for comment in downloader.get_comments_from_url(url):
            comment['video_id'] = video_id
            results.append(comment)
    except Exception as e:
        print(f"{video_id} 에서 오류 발생: {e}")

# 데이터프레임으로 만들기
df = pd.DataFrame(results)
# CSV로 저장
df.to_csv('youtube_comments.csv', index=False, encoding='utf-8-sig')
print('댓글 추출 완료 및 파일 저장!')
