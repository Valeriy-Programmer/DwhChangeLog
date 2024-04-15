<template>
    <div>
        <h1>{{ name }}</h1>

        <div>
            <table>
                <tr>
                    <th>Название</th>
                    <th>Значение</th>
                </tr>

                <tr v-for="i in 50" :key="i">
                    <td>{{ i }}</td>
                    <td>{{ i }}</td>
                </tr>
            </table>
        </div>

    </div>
</template>

<script>export default {
  name: 'PIM_v_1',
  props: {
      name: String
  }
}</script>

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
</style>
