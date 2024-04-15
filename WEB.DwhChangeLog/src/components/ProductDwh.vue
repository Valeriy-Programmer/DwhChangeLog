<template>
    <div class="hello">
        <h1>{{ name }}</h1>
        <!--<div v-if="product">{{ product }}</div>-->
        <!--<div v-if="changeLog">{{ changeLog }}</div>-->
    <div v-if="groupedChangeLog">{{ groupedChangeLog }}</div>
        
        <!--<table border="1">
    <tr>
        <th>Author ID</th>-->
        <!--<th>Directory ID</th>-->
        <!--<th>Change Log Type</th>-->
        <!--<th>Change Log Record ID</th>-->
        <!--<th>Change Log Data</th>
        <th>Date</th>
    </tr>
    <tr v-for="item in changeLog" :key="item.id">
        <td>{{ item.attributes.author_id }}</td>-->
        <!--<td>{{ item.attributes.directory_id }}</td>-->
        <!--<td>{{ item.attributes.change_log_type }}</td>-->
        <!--<td>{{ item.attributes.change_log_record_id }}</td>-->
        <!--<td>
                <ul>
                    <li v-for="(value, key) in item.attributes.change_log_data" :key="key">
                        <strong>{{ key }}:</strong> {{ value }}
                    </li>
                </ul>
            </td>
            <td>{{ item.attributes.dt_create }}</td>
        </tr>
    </table>-->

    <div v-for="(item, index) in changeLog" :key="item.id" class="info">
        <div class="log-item">
            <!--<p>{{ item.attributes.change_log_type }}: {{ Object.keys(item.attributes.change_log_data)[0] }}</p>-->
            <p><span class="log-attribute">{{ Object.keys(item.attributes.change_log_data)[0] }}</span></p>
            <p>Автор Id: {{ item.attributes.author_id }} <span class="log-date">дата: {{ item.attributes.dt_create }}</span></p>
            <p>Старое значение:</p>
            <p>{{ Object.values(item.attributes.change_log_data)[0] }}</p>
            <p>Новое значение:</p>
            <p v-if="index < changeLog.length - 1">
                {{ Object.values(changeLog[index + 1].attributes.change_log_data)[0] }}
            </p>
        </div>
    </div>

        <table border="1" v-if="product">
            <tr v-if="product">
                <th>Название</th>
                <th>Значение</th>
            </tr>

            <tr v-for="(value, key) in product.attributes" :key="key">
                <td>{{ key }}</td>
                <td>{{ value }}</td>
            </tr>
        </table>
    </div>
</template>

<script>
    import axios from 'axios';

    export default {
        name: 'ProductDwh',
        props: {
            name: String
            },

        data() {
                return {
                    product: null
                };
            },

        mounted() {
            // Установка заголовков
            const headers = {
                'Accept': 'application/vnd.api+json', // пример значения для заголовка Accept
                'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwczovL2FwaS5kd2guYTkxMS51YS9sb2dpbiIsImlhdCI6MTcwODM0MTk1MiwiZXhwIjoxNzA4MzcwNzUyLCJuYmYiOjE3MDgzNDE5NTIsImp0aSI6IlBBQ2hFV0xOVEpibTMxM1EiLCJzdWIiOiI0OSIsInBydiI6IjE2ZTRjZGEzNThkYjRmNzI0MWUyODc3MTYwZmIxODJlNTBjYTZkZmUiLCJ1aSI6ZmFsc2UsInJvbGUiOiI1MjY1NzM3NSIsImNvcyI6bnVsbCwiZ29vZ2xlMmZhIjpmYWxzZX0.fNkuN_CxdQRBf4yw3cGJh2PLP7ECpS1dw3ifB3PTxuw' // пример значения для заголовка Authorization
            };

            axios.get('https://api.dwh.a911.ua/product/50423', { headers })
                .then(response => {
                    // Обработка успешного ответа
                    this.product = response.data.data;
                })
                .catch(error => {
                    // Обработка ошибки
                    console.error('Ошибка при выполнении GET запроса:', error);
                });

            axios.get('https://api.dwh.a911.ua/change-logs?filter[directory_id]=1&filter[change_log_record_ids]=50423&sort=-dt_create', { headers })
                .then(response => {
                    // Обработка успешного ответа
                    this.changeLog = response.data.data.slice().reverse();
                    const groupedData = {};
                    this.changeLog.forEach(item => {
                        const key = item.attributes.change_log_data ? Object.keys(item.attributes.change_log_data)[0] : "null";
                        if (!groupedData[key]) {
                            groupedData[key] = [];
                        }
                        groupedData[key].push(item);
                    });
                    this.groupedChangeLog = groupedData;
                })
                .catch(error => {
                    // Обработка ошибки
                    console.error('Ошибка при выполнении GET запроса:', error);
                });
        }
     }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
    .info {
        text-align: left;
    }
    .log-item {
        margin-bottom: 40px;
    }
    .log-attribute {
        font-weight: bold;
    }
    .log-date {
        color: darkgray;
    }
</style>
