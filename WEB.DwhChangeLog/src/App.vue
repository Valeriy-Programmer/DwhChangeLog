<!--<!DOCTYPE html>
<html>
<head>
    <base target="_top">
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css">
</head>
<body>

    <div id="app">
        <PIM_v_1 name="PIM_v_1" />
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/js/materialize.min.js"></script>

    <script src="./components/PIM_v_1.vue"></script>

</body>
</html>-->

<template>

    <!-- Navbar -->
    <div class="navbar-fixed">
        <nav>
            <div class="nav-wrapper blue-grey darken-4">

                <ul id="nav-mobile" class="left hide-on-med-and-down">
                    <li><a href="#">PIM v.1</a></li>
                    <li><a href="#">Товары</a></li>
                    <li><a href="#">Партнеры</a></li>
                    <li><a href="#">Аптеки</a></li>
                </ul>

                <!-- Additional Menu -->
                <a class='dropdown-trigger btn' href='#' id="additionalMenu" data-target='additionalMenuDropdown' style="position: absolute; bottom: 0; right: 0; margin-bottom: 3px; height: 19px;"><i class="Small material-icons" style="position: absolute; bottom: -24px; right: 2px;">expand_more</i></a>
                <ul id='additionalMenuDropdown' class='dropdown-content'>
                    <li><a href="#!"><i class="material-icons">file_upload</i>Экспорт</a></li>
                    <li><a href="#!"><i class="material-icons">file_download</i>Импорт</a></li>
                    <li class="divider" tabindex="-1"></li>
                    <li><a href="#!"><i class="material-icons">filter_list</i>Фильтры</a></li>
                    <li><a href="#!"><i class="material-icons">assignment</i>Логи</a></li>
                    <li><a href="#!"><i class="material-icons">view_list</i>Отчет</a></li>
                    <li class="divider" tabindex="-1"></li>
                    <li><a href="#!"><i class="material-icons">wrap_text</i>Источники</a></li>
                </ul>

            </div>
        </nav>
    </div>

    <!-- Page Layout -->
    <div class="row">

        <div class="col s12 m4 l3" style="width: 250px">
            <!-- Navigation Panel -->

            <ul id="slide-out" class="sidenav sidenav-fixed" style="top: 64px; width: 210px">
                
                <div class="row">
                    <div class="col s12">
                        <div class="row">
                            <div class="input-field col s12">
                                <i class="material-icons prefix">search</i>
                                <input type="text" id="searchSidebarMenu" class="autocomplete">
                                <label for="searchSidebarMenu">Autocomplete</label>
                            </div>
                        </div>
                    </div>
                </div>

                <li class="no-padding">
                    <ul class="collapsible collapsible-accordion">
                        <li>
                            <a class="collapsible-header">Администрирование<i class="material-icons" style="margin:0px">arrow_drop_down</i></a>
                            <div class="collapsible-body">
                                <ul>
                                    <li><a href="#">Пользователи</a></li>
                                    <li><a href="#">Правила по умолчанию</a></li>
                                    <li><a href="#">Уникальные правила</a></li>
                                    <li><a href="#">Модуль переводов</a></li>
                                </ul>
                            </div>
                        </li>
                        <li>
                            <a class="collapsible-header">Товары<i class="material-icons" style="margin:0px">arrow_drop_down</i></a>
                            <div class="collapsible-body">
                                <ul>
                                    <li><a href="#">Товары</a></li>
                                    <li><a href="#">Бренды</a></li>
                                    <li><a href="#">Производители</a></li>
                                    <li><a href="#">Заявители</a></li>
                                </ul>
                            </div>
                        </li>
                    </ul>
                </li>
            </ul>
        </div>

    <!-- Content -->
    <div class="col s12 m8 l9">
        <div class="row">
            <div class="input-field col s6">
                <input placeholder="Placeholder" id="fn" type="text" class="validate">
                <label for="fn">First Name</label>
            </div>
            <div class="input-field col s6">
                <input id="ln" type="text" class="validate">
                <label for="ln">Last Name</label>
            </div>
        </div>
        <div class="row">
            <div class="input-field col s12">
                <select id="app">
                    <option disabled selected>Choose your app</option>
                    <option>Google Shit</option>
                    <option>Excell</option>
                    <option>Other</option>
                </select>
                <label>Application</label>
            </div>
        </div>
        <div class="row">
            <button class="waves-effect waves-light btn-small"><i class="material-icons left">chevron_right</i>Поиск</button>
        </div>

        <PIM_v_1 name="PIM_v_1" />
    </div>
    </div>


</template>

<script>
    import PIM_v_1 from './components/PIM_v_1.vue';
    import M from 'materialize-css/dist/js/materialize.min';

    export default {
        name: 'App',
        components: {
            PIM_v_1,
        },
        mounted() {
            M.AutoInit();

            var additionalMenu = document.getElementById('additionalMenu');
            var instanceAdditionalMenu = M.Dropdown.getInstance(additionalMenu);
            var additionalMenuDropdown = document.getElementById('additionalMenuDropdown');
            instanceAdditionalMenu.options.onOpenStart = function () {
                setTimeout(function () {
                    additionalMenuDropdown.style.top = '68px'; // Устанавливаем стиль top
                }, 1); // Устанавливаем задержку в 1 миллисекунду 
            };

            var searchSidebarMenu = document.getElementById('searchSidebarMenu');
            var instanceSearchSidebarMenu = M.Autocomplete.getInstance(searchSidebarMenu);
            instanceSearchSidebarMenu.options.data = {
                "Apple": null,
                "Microsoft": null,
                "Google": 'https://placehold.it/250x250'
            }
            
        }
    }

</script>

<style>

    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
    }

    .collapsible-body a  {
        text-align: left;
    }

    .collapsible-header {
        text-align: left;
    }

</style>
