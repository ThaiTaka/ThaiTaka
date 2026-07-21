<div align="center">
  <a href="https://git.io/typing-svg">
    <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=28&pause=1000&color=00FF00&center=true&vCenter=true&width=600&lines=Hi+there,+I'm+Taka+👋;Final-year+IT+Student;Game+%26+Web3D+Developer;AI+%2F+Machine+Learning+Enthusiast" alt="Typing SVG" />
  </a>
</div>

<br/>

### 👨‍💻 Về bản thân (Terminal View)

```json
{
  "name": "Lê Thành Thái",
  "alias": "Taka",
  "status": "Năm cuối Công nghệ Thông tin",
  "focus": [
    "Web 3D & Frontend Architecture", 
    "Game Development",
    "Computer Vision & Data Science"
  ],
  "current_projects": {
    "TakaVision": "Hệ thống quản lý nội dung 3D portfolio (Next.js, Sanity.io)",
    "The Call Beneath": "Game khám phá đáy biển giải đố mã Morse (Unity 3D)"
  },
  "activities": [
    "Training YOLOv8 models",
    "Kaggle Machine Learning Competitions",
    "Teaching programming to my students"
  ]
}
name: generate animation

on:
  # Chạy mỗi ngày vào lúc 0 giờ
  schedule:
    - cron: "0 0 * * *" 
  
  # Chạy thủ công bất cứ lúc nào
  workflow_dispatch:
  
  # Chạy khi có commit mới lên branch main
  push:
    branches:
    - main
    
jobs:
  generate:
    permissions: 
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 10
    
    steps:
      # Chú rắn bò để tạo ra các file SVG
      - name: generate github-contribution-grid-snake.svg
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ThaiTaka
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark
          
      # Đẩy các file SVG được tạo ra lên một branch đặc biệt (gọi là 'output')
      - name: push github-contribution-grid-snake.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
