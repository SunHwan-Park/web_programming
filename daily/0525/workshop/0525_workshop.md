# 0525_workshop

- `get_cat_image_vue.html`

    ```html
    <!DOCTYPE html>
    <html lang="ko">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>0525 workshop</title>
    </head>
    <body>
        <div id="app">
            <h1>Cat Image</h1>
            <img :src="imgURL" style="height: 300px">
            <hr>
            <button @click="getCatImage">고양이 사진 교체</button>
        </div>
        <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script>
            const app = new Vue({
                el: '#app',
                data: {
                    imgURL: ''
                },
                methods: {
                    getCatImage() {
                        const catURL = 'https://api.thecatapi.com/v1/images/search'
                        axios.get(catURL)
                            .then(response => {
                                this.imgURL = response.data[0].url
                            })
                    }
                }
            })
        </script>
    </body>
    </html>
    ```
