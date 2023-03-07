<template>
  <div class="subtitle">The Editable Homepage</div>
  <div id="about">
    Anyone can edit any part of the homepage. No account required.<br>
    <br>
    All text is auto-saved as you type. If you find something you find offensive, just delete it.<br>
    <br>
    Publichomepage is <a class="link" href="https://github.com/routman/publichomepage.com" target="_blank" rel="noopener">open source</a> and offered as a free service. Your cryptocurrency donations support operating costs and are greatly appreciated.<br>
    <br>
    BTC: bc1q7fqwmtq2vaka8wwpjpnmlehe36qrgfmlw33vh9<br>
    <br>
    LTC: LYMSJ313xJaUsAmucuYRkVJmGB8Ut9VDz8<br>
    <br>
    DOGE: DATumCTp1QBG1Gpa3ko6bXPXccnFMFDgYC<br>
    <br>
    ETH: 0x6abD6f3df07c06e4137269D7187661dE37441218<br>
    <br>
    publichomepage &copy; {{ new Date().getFullYear() }}<br>
    <br>
  </div>
</template>

<script>

export default {
  name: 'about'
}
</script>

<style scoped lang="scss">
@import "../assets/settings.scss";

#about {
  flex-grow: 1;
  overflow-y: scroll;
  -ms-overflow-style: none;
  scrollbar-width: none;
  -webkit-overflow-scrolling: touch;
}

@media (prefers-color-scheme: dark) {

}

</style>
