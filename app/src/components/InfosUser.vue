<template>
  <Transition mode="out-in">
    <main v-if="dataUser?.id">
      <div class="img-container">
        <img
          width="200"
          height="200"
          :src="dataUser.avatar_url"
          :alt="dataUser.name"
        />
        <ul class="profile-details">
          <li>
            <svg width="22" height="22" viewBox="0 0 256 256">
              <path
                fill="#6f768d"
                d="m141.7 133.7l-42 42A8.3 8.3 0 0 1 94 178a7.7 7.7 0 0 1-3-.6a8 8 0 0 1-5-7.4v-34H24a8 8 0 0 1 0-16h62V86a8 8 0 0 1 5-7.4a8.2 8.2 0 0 1 8.7 1.7l42 42a8.1 8.1 0 0 1 0 11.4ZM192 32h-56a8 8 0 0 0 0 16h56v160h-56a8 8 0 0 0 0 16h56a16 16 0 0 0 16-16V48a16 16 0 0 0-16-16Z"
              />
            </svg>
            <span>{{ formatDate(dataUser.created_at) }}</span>
          </li>

          <li>
            <svg width="22" height="22" viewBox="0 0 256 256">
              <path
                fill="#6f768d"
                d="M195.9 195.9a96.1 96.1 0 0 1-135.8 0a8 8 0 0 1 0-11.3a7.9 7.9 0 0 1 11.3 0a80 80 0 1 0 0-113.2l-4.3 4.3l18.4 18.4a8 8 0 0 1-5.7 13.6h-48a8 8 0 0 1-8-8v-48a8.2 8.2 0 0 1 5-7.4a8 8 0 0 1 8.7 1.8l18.3 18.3l4.3-4.3a96 96 0 0 1 135.8 135.8Z"
              />
            </svg>
            <span>{{ formatDate(dataUser.updated_at) }}</span>
          </li>

          <li>
            <svg width="22" height="22" viewBox="0 0 256 256">
              <path
                fill="#6f768d"
                d="M128.1 64a40 40 0 1 0 40 40a40.1 40.1 0 0 0-40-40Zm0 64a24 24 0 1 1 24-24a24.1 24.1 0 0 1-24 24Zm0-112a88.1 88.1 0 0 0-88 88c0 31.4 14.5 64.7 42 96.2a259.4 259.4 0 0 0 41.4 38.4a8.3 8.3 0 0 0 9.2 0a257.6 257.6 0 0 0 41.5-38.4c27.4-31.5 41.9-64.8 41.9-96.2a88.1 88.1 0 0 0-88-88Zm0 206c-16.5-13-72-60.8-72-118a72 72 0 0 1 144 0c0 57.2-55.5 105-72 118Z"
              />
            </svg>
            <span>{{ dataUser.location }}</span>
          </li>
        </ul>
      </div>

      <div class="profile-infos">
        <div class="profile-essential-infos">
          <h1>{{ dataUser.name }}</h1>
          <a class="login" :href="dataUser.html_url">@{{ dataUser.login }}</a>
          <p class="bio" v-if="dataUser.bio">{{ dataUser.bio }}</p>
          <p v-else>Este perfil não possui uma bio.</p>
        </div>

        <ul class="profile-stats">
          <li>
            <span>Repositórios</span>
            <p>{{ dataUser.public_repos }}</p>
          </li>

          <li>
            <span>Seguidores</span>
            <p>{{ dataUser.followers }}</p>
          </li>

          <li>
            <span>Seguindo</span>
            <p>{{ dataUser.following }}</p>
          </li>
        </ul>
      </div>
    </main>
  </Transition>
</template>

<script>
export default {
  name: "InfosUser",
  props: ["dataUser"],

  setup() {
    function formatDate(date) {
      const newDate = new Date(date);
      return newDate.toLocaleDateString("pt-BR", {
        year: "numeric",
        month: "long",
        day: "numeric",
      });
    }
    return { formatDate };
  },
};
</script>

<style scoped lang="scss">
@import "../scss/abstracts/mixins.scss";

main {
  display: grid;
  grid-template-columns: auto 1fr;
  align-content: start;
  gap: 30px;
  max-width: 100%;
  background: #fff;
  border-radius: 12px;
  box-shadow: 0px 0px 10px #cbcfe4;
  padding: 40px;
  @include responsive("medium") {
    grid-template-columns: 1fr;
    align-items: center;
    padding: 20px;
  }
}

.img-container {
  min-width: max-content;

  img {
    max-width: 200px;
    border-radius: 50%;
    margin-bottom: 10px;
    filter: drop-shadow(0px 5px 10px #9da3c0);
  }

  .profile-details {
    display: flex;
    flex-direction: column;
    gap: 2px;

    li {
      display: flex;
      align-items: center;
      gap: 5px;
    }
  }
  @include responsive("medium") {
    justify-self: center;
    li {
      justify-content: center;
    }
  }
}

.profile-stats {
  display: flex;
  justify-content: center;
  gap: 20px;
  background: #f5f5f5;
  border-radius: 8px;
  padding: 10px 20px;

  li {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 5px;

    p {
      font-size: 2rem;
      font-weight: bold;
    }
  }
}

.profile-infos {
  .profile-essential-infos {
    margin-bottom: 20px;

    h1 {
      letter-spacing: -1px;
    }

    .login {
      display: inline-block;
      font-size: 20px;
      color: #467ca2;
      margin-bottom: 20px;
      &:hover {
        text-decoration: underline;
      }
    }

    .bio {
      max-width: 35ch;
    }

    @include responsive("medium") {
      display: flex;
      flex-direction: column;
      align-items: center;

      .bio {
        text-align: center;
      }
    }
  }
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
  transform: translateY(-30px);
}

.v-enter-active,
.v-leave-active {
  transition: 0.3s;
}
</style>
