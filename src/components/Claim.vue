<template>
  <div class="claimwrapper">
    <h1 class="claim"><b>SPACER <small>v 0.1.0</small></b></h1>
    <p class="sub-claim">
      Rozpocznij swoją podróż przez wspaniałą galaktykę i odkrywaj miejsca o których nawet nie
      słyszałeś.
    </p>
    <p class="sub-claim">Wpisz cokolwiek związanego z kosmosem.</p>
  </div>
</template>

<script>
export default {
  name: 'Claim',
};
</script>

<style lang="scss" scoped>
.claimwrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  color: #fafafa;
  padding-bottom: 30px;

  @media (min-width: 768px) {
    zoom: 1.4;
    padding-bottom: 60px;
  }
}

.claim {
  font-size: 50px;
  margin: 0;
}

.sub-claim {
  margin-bottom: 0;
}
</style>
