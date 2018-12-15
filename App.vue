<template>
    <div>
        <label for='personal-data'>
            Upload SongsterrPersonalData.json
        </label>
        <input
            type='file'
            id='personal-data'
            @change='file'
        >
        <button
            @click='example'
        >
            See an example
        </button>
        <template v-if='data'>
            <ul>
                <li
                    v-for='(upload, index) in data.uploads'
                    :key='index'
                >
                <!-- "id": 95447,
            "comment": "Initial revision",
            "artist": "5 Diez",
            "song": "Спрут",
            "difficulty": "Intermediate",
            "url": "http://d12drcwhcokzqv.cloudfront.net/5697621.gp5" -->
                    <p>
                        {{ upload.id }}
                    </p>
                    <p>
                        {{ upload.comment }}
                    </p>
                    <p>
                        {{ upload.artist }}
                    </p>
                    <p>
                        {{ upload.song }}
                    </p>
                    <p>
                        {{ upload.difficulty }}
                    </p>
                    <p>
                        <a
                            :href='upload.url'
                            download
                        >
                            Download
                        </a>
                    </p>
                </li>
            </ul>
        </template>
    </div>
</template>
<script>
    import example from './SongsterrPersonalData.json'
    export default {
        data() {
            return {
                data: null,
            }
        },
        methods: {
            file(event) {
                const file = event.target.files[0]
                const reader = new FileReader()
                reader.onload = (theFile => event => {
                    const result = event.target.result
                    this.data = JSON.parse(result)
                })(file)
                reader.readAsText(file)
            },
            example() {
                this.data = example
            }
        }
    }
</script>
