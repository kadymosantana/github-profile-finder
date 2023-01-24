<template>
  <main>
    <div class="img-container">
      <img
        width="200"
        height="200"
        :src="dataUser.avatar_url"
        :alt="dataUser.name"
      />
      <ul class="profile-details">
        <li>
          <img src="@/assets/icons/created_at.svg" alt="" />
          <span>{{ formatDate(dataUser.created_at) }}</span>
        </li>

        <li>
          <img src="@/assets/icons/updated_at.svg" alt="" />
          <span>{{ formatDate(dataUser.updated_at) }}</span>
        </li>

        <li>
          <img src="@/assets/icons/location.svg" alt="" />
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
</template>

<script setup>
const props = defineProps(["dataUser"]);

const formatDate = (date) => {
  const newDate = new Date(date);
  return newDate.toLocaleDateString("pt-BR", {
    year: "numeric",
    month: "long",
    day: "numeric",
  });
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

  > img {
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
</style>
