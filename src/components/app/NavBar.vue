<template>
    <nav class="navbar orange lighten-1">
        <div class="nav-wrapper">
            <div class="navbar-left">
                <a href="#" @click.prevent="$emit('clickMenu')">
                    <i class="material-icons black-text">dehaze</i>
                </a>
                <span class="black-text">{{ date }}</span>
            </div>

            <ul class="right hide-on-small-and-down">
                <li>
                    <a class="dropdown-trigger black-text" href="#" data-target="dropdown"
                    ref="dropdown">
                        USER NAME
                        <i class="material-icons right">arrow_drop_down</i>
                    </a>

                    <ul id='dropdown' class='dropdown-content'>
                        <li>
                            <router-link to="/profile" class="black-text">
                                <i class="material-icons">account_circle</i>Профиль
                            </router-link>
                        </li>
                        <li class="divider" tabindex="-1"></li>
                        <li>
                            <a href="#" class="black-text" @click.prevent="logout">
                                <i class="material-icons">assignment_return</i>Выйти
                            </a>
                        </li>
                    </ul>
                </li>
            </ul>
        </div>
    </nav>
</template>

<script>
import M from 'materialize-css/dist/js/materialize.min';

export default {
    computed: {

    },
    data: () => ({
        date: null,
        interval: null,
        dropdown: null,
        dateOptions: {
            hour: '2-digit',
            minute: '2-digit',
            second: '2-digit',

            hours12: false,

            weekday: 'long',
            day: 'numeric',
            month: 'long',
            year: 'numeric',
        }
    }),
    methods: {
        logout() {
            console.log('logout')
            this.$router.push('/login?message=logout')
        },
    },
    mounted() {
        this.dropdown = M.Dropdown.init(this.$refs.dropdown, {
            constrainWidth: true
        }),
        this.interval = setInterval(() => {
            this.date = new Intl.DateTimeFormat('ru-RU', this.dateOptions).format()
        }, 1000)
    },
    beforeUnmount() {
        clearInterval(this.interval)
        if (this.dropdown && this.dropdown.destroy) {
            this.dropdown.destroy()
        }
    }
}
</script>