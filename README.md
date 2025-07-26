<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>생각 나누기 보드</title>
    <style>
      body {
        font-family: sans-serif;
        max-width: 800px;
        margin: 2rem auto;
        padding: 1rem;
      }
      textarea {
        width: 100%;
        height: 100px;
        margin-bottom: 1rem;
      }
      input[type="file"] {
        margin-bottom: 1rem;
      }
      .post {
        border: 1px solid #ccc;
        border-radius: 10px;
        padding: 1rem;
        margin-bottom: 1rem;
      }
      .post img {
        max-width: 200px;
        display: block;
        margin-top: 1rem;
      }
      button {
        padding: 0.5rem 1rem;
        font-size: 1rem;
        cursor: pointer;
      }
    </style>
  </head>
  <body>
    <h1>생각 나누기 보드</h1>
    <textarea id="content" placeholder="여기에 생각을 입력하세요"></textarea>
    <br />
    <input type="file" id="imageInput" accept="image/*" />
    <br />
    <button onclick="handlePost()">올리기</button>

    <div id="posts"></div>

    <script>
      const postsContainer = document.getElementById("posts");
      const contentInput = document.getElementById("content");
      const imageInput = document.getElementById("imageInput");

      function handlePost() {
        const content = contentInput.value.trim();
        if (!content) return;

        const postDiv = document.createElement("div");
        postDiv.className = "post";

        const contentP = document.createElement("p");
        contentP.textContent = content;
        postDiv.appendChild(contentP);

        const file = imageInput.files[0];
        if (file) {
          const reader = new FileReader();
          reader.onloadend = () => {
            const img = document.createElement("img");
            img.src = reader.result;
            postDiv.appendChild(img);
            postsContainer.prepend(postDiv);
          };
          reader.readAsDataURL(file);
        } else {
          postsContainer.prepend(postDiv);
        }

        contentInput.value = "";
        imageInput.value = null;
      }
    </script>
  </body>
</html>
