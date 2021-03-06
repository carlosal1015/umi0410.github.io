# [umi0410.github.io](https://umi0410.github.io)
![README_preview.png](static/README_preview.png)

## About this blog

* 글 적는 법
  * Project root에서
  ```bash
  $ hugo new --kind chapter {{*.md_FILE_REL_PATH_ABOUT_/content/}}
  ```
  * 개발용(초안)으로 적는 글은 .Page.Params의 draft: true로 설정 후 `hugo serve -D`를 통해
    draft 상태인 글도 볼 수 있다. 
* 배포 자동화
  * branch:master에서 게시글 작성
  * branch:**에 push할 경우 Github Action을 통해 빌드
  * 빌드된 파일은 branch:gh-pages에 배포~! (Github Page가 gh-pages 브랜치를 바라보기 때문.)
* 재미삼아 개발 중~!


## Customization
themes/hugo-theme-learn 을 바탕으로 몇몇 부분을 수정해서 운영하고있다.
submodule을 통해 원본 theme은 유지하고 `layout` directory를 수정함으로써 오버라이드하거나 커스터마이징 중이다.

* `layouts/partials/` 에서 몇몇 html 추가 및 오버라이드
  * `custom-sidebar-profile.html` 에 프로필을 추가.
  * `menu.html` 에서 `custom-sidebar-profile` 을 import
  * `custom-comments.html` 에 disqus 관련 설정 추가
    ```html
    {{ if not .Params.noDisqus }}
    {{ template "_internal/disqus.html" . }}
    {{ end }}
    ```
    각각의 페이지에서 parameter로 disqus를 비활성화하려면 .Page.Params로 `noDisqus: true`를 정의해준다.
  * `favicon.html`에서 favicon을 `https://emojipedia-us.s3.dualstack.us-west-1.amazonaws.com/thumbs/120/google/241/whale_1f40b.png` 로 설정
  * `custom-footer.html`에 Google Analytics 설정 추가

* `layouts/shortcodes/` 을 변경
  * `toc.html`을 이용해 각 페이지에서 내용을 요약하기 위한 Table of Contents 기능을 추가함.

* `statics/css/` 에서 몇몇 css 추가 및 오버라이
  * `theme-umi0410-blue.css` 를 통해 `learn theme` 의 css를 수정한 Custom theme 정의
    * 기본적인 테마의 색상 변경
    * \<code\>에 대한 색상 변경
  * `custom-umi0410.css` 에서 부가적이고 잡다한 css 변경. 테마 자체에 대한 것 외의 css 수정사항은 거의 이곳에 위치.
    * 페이지 헤더의 브레드크럼의 토글되는 Table of Contents 부분인 `.progress` 에대한 수정


## Refs and Tips

* [hugo-theme-learn docs](https://learn.netlify.app/en/)

* [Useful short codes](https://learn.netlify.app/en/shortcodes/)

* [Markdown image resizing](https://learn.netlify.app/en/cont/markdown/#resizing-image)

* local에서 disqus가 이용되지 않는 경우
  * [localtest.me란](https://superuser.com/questions/1280827/why-does-the-registered-domain-name-localtest-me-resolve-to-127-0-0-1)
  * trusted domains 에 [localtest.me](localtest.me) 추가하기
* [google search console](https://search.google.com/search-console/sitemaps) 설정
  * static/robots.txt 작성