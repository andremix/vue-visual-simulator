<template>
  <ul class="ul-item-list">
    <li
      v-for="(item, index) in items"
      v-show="item.name.toLowerCase().includes(item_filter.toLowerCase())"
      class="li-item"
      :key="item.id"
    >
      <img
        :src="
          'https://static.divine-pride.net/images/items/item/' +
          item.id +
          '.png'
        "
        class="img-item"
        :class="{
          'item-selected': parseInt(item.id) == $store.state.headgear_mid_id,
          'item-disabled': parseInt(item.viewID) == 0,
        }"
        :viewID="item.viewID"
        :id="item.id"
        data-bs-toggle="tooltip"
        data-bs-placement="top"
        :title="item.name"
        :name="item.name"
        @click="clickItem($event)"
      />
    </li>
  </ul>
</template>

<script>
import { mapMutations } from "vuex";

export default {
  name: "ItemListHeadMid",
  props: ["item_filter"],
  data() {
    return {
      items: [
        { id: 0, name: "X", viewID: 0 },
        { id: 19830, name: "Óculos Hi-Ban", viewID: 12 },
        { id: 31487, name: "Tapa-Olho Pirata", viewID: 13 },
        { id: 31155, name: "Óculos de Nerd", viewID: 27 },
        { id: 19638, name: "Sr. Sorriso", viewID: 65 },
        { id: 19551, name: "Símbolo Élfico", viewID: 73 },
        { id: 19734, name: "Amplificador Ocular", viewID: 83 },
        { id: 20142, name: "Óculos de Motociclista", viewID: 92 },
        { id: 19735, name: "Presilhas de Barbatana", viewID: 100 },
        { id: 19550, name: "Bochechas Coradas", viewID: 125 },
        { id: 19679, name: "Cara de Espanto", viewID: 185 },
        { id: 5329, name: "Venda Legítima da Takius", viewID: 187 },
        { id: 410011, name: "Venda Sombrosa", viewID: 187 },
        { id: 31570, name: "Visor Futurista", viewID: 207 },
        { id: 19554, name: "Máscara Tradicional", viewID: 230 },
        { id: 19680, name: "Máscara da Criança Travessa", viewID: 253 },
        { id: 20166, name: "Máscara do Jay Zon", viewID: 336 },
        { id: 20145, name: "Visor do Ciborgue", viewID: 345 },
        { id: 20146, name: "Máscara da Deusa", viewID: 394 },
        { id: 19801, name: "Máscara da ANBU", viewID: 403 },
        { id: 19722, name: "Óculos Intelectuais", viewID: 404 },
        { id: 19769, name: "Orelhas de Fada Travessa", viewID: 405 },
        { id: 19810, name: "Orelhas de Ifrit", viewID: 422 },
        { id: 19877, name: "Olho do Beholder", viewID: 467 },
        { id: 19669, name: "Legado de Reginleif", viewID: 468 },
        { id: 19919, name: "Máscara de Quve", viewID: 472 },
        { id: 19924, name: "Máscara de Odin", viewID: 480 },
        { id: 19826, name: "Asinhas do Inverno", viewID: 584 },
        { id: 31184, name: "Tapa-Olho do Falcão", viewID: 609 },
        { id: 20391, name: "Silenciador", viewID: 632 },
        { id: 19954, name: "Óculos Visuais 3D", viewID: 661 },
        { id: 31262, name: "Óculos Descartáveis", viewID: 661 },
        { id: 20144, name: "Orelhas de Elfo Ancestral", viewID: 665 },
        { id: 20126, name: "Máscara de Thanatos", viewID: 667 },
        { id: 19534, name: "Rosto do Despero", viewID: 693 },
        { id: 19509, name: "Asas de Borboleta", viewID: 695 },
        { id: 19510, name: "Parafusos Soltos", viewID: 696 },
        { id: 19511, name: "Tapa-Olho Estiloso", viewID: 697 },
        { id: 19512, name: "Tapa-Olho Fashion", viewID: 698 },
        { id: 19542, name: "Fantasma Travesso", viewID: 712 },
        { id: 31327, name: "Nariz de Galho", viewID: 737 },
        { id: 20215, name: "Máscara Macabra", viewID: 760 },
        { id: 31505, name: "Falcoelmo", viewID: 782 },
        { id: 19925, name: "Monóculo Gótico", viewID: 807 },
        { id: 20108, name: "Óculos Julieta de Quartzo Rubi", viewID: 813 },
        { id: 20314, name: "Óculos da Gaga", viewID: 856 },
        { id: 20311, name: "Fone da Ratishune Meeku", viewID: 873 },
        { id: 20136, name: "Orelhas dos 11 Anos e um Segredo", viewID: 875 },
        { id: 18742, name: "Luar de Cristal", viewID: 881 },
        { id: 18744, name: "Gotas da Via Láctea", viewID: 883 },
        { id: 20221, name: "Venda Macabra", viewID: 886 },
        { id: 20077, name: "Óculos Glamorosos", viewID: 925 },
        { id: 20230, name: "Máscara da Falência", viewID: 936 },
        { id: 20295, name: "Visor de Quartzo-Poring", viewID: 954 },
        { id: 31118, name: "Máscara do Vilão", viewID: 984 },
        { id: 20312, name: "Olho Maligno do Barão", viewID: 989 },
        { id: 19752, name: "Asinhas Elegantes", viewID: 990 },
        { id: 19776, name: "Orelhas de Fada Animada", viewID: 998 },
        { id: 31561, name: "Asas de Dragão Sombrio", viewID: 1008 },
        { id: 31534, name: "Tiara Colorida", viewID: 1019 },
        { id: 19787, name: "Olhos de Valquíria", viewID: 1021 },
        { id: 31380, name: "Corvo Fofoqueiro", viewID: 1035 },
        { id: 5912, name: "Deviling Companheiro", viewID: 1036 },
        { id: 20376, name: "Presilha dos Amantes", viewID: 1072 },
        { id: 19871, name: "Ritmo do Momento", viewID: 1074 },
        { id: 19882, name: "Vaso de Planta Anti-Z", viewID: 1086 },
        { id: 19912, name: "Olhos Felinos", viewID: 1100 },
        { id: 410053, name: "Óculos de Sol Estiloso", viewID: 1169 },
        { id: 31527, name: "Asas Presilhas", viewID: 1186 },
        { id: 20010, name: "Orelhas Solares", viewID: 1198 },
        { id: 20047, name: "Guizos de Cerejeira", viewID: 1223 },
        { id: 31902, name: "Óculos das Lentes Vivas", viewID: 1237 },
        { id: 20101, name: "Asas de Bragi", viewID: 1241 },
        { id: 31183, name: "Asas Grafite", viewID: 1250 },
        { id: 20116, name: "Fones de Sereia", viewID: 1254 },
        { id: 20115, name: "Óculos do Sabe-Tudo", viewID: 1255 },
        { id: 20131, name: "Fone dos Vocalroks", viewID: 1266 },
        { id: 20154, name: "Folhas Outonais", viewID: 1275 },
        { id: 20399, name: "Fantasia do Tengu Corvo", viewID: 1287 },
        { id: 20176, name: "Máscara Feliz do Pierrot", viewID: 1288 },
        { id: 20195, name: "Gato Rabugento", viewID: 1292 },
        { id: 20246, name: "Ilusões do Tempo", viewID: 1309 },
        { id: 20255, name: "Candura do Amor", viewID: 1318 },
        { id: 20298, name: "Orelhas Brancas de Lunático", viewID: 1340 },
        { id: 20299, name: "Torta de Baunilha", viewID: 1341 },
        { id: 20318, name: "Fones do Pikachiu", viewID: 1354 },
        { id: 20319, name: "Fone da Megarine Louca", viewID: 1355 },
        { id: 20325, name: "Aura de Byalan", viewID: 1363 },
        { id: 19289, name: "Tapa-Lua", viewID: 1370 },
        { id: 20379, name: "Presilha de Relógio Retrô", viewID: 1404 },
        { id: 31609, name: "Máscara do Aristocrata", viewID: 1409 },
        { id: 20397, name: "Máscara de Jakk", viewID: 1415 },
        { id: 20406, name: "Chapéu de Andrômeda", viewID: 1417 },
        { id: 20459, name: "Coroa Colorida", viewID: 1423 },
        { id: 20430, name: "Crânios Etéreos de Morroc", viewID: 1440 },
        { id: 31540, name: "Lentes Gemini", viewID: 1456 },
        { id: 31483, name: "Adereço de Gatinho", viewID: 1472 },
        { id: 31375, name: "Olhos Macabros", viewID: 1490 },
        { id: 31047, name: "Bochechas da Paixão", viewID: 1494 },
        { id: 31120, name: "Orelhas de Vampiro", viewID: 1548 },
        { id: 31122, name: "Bandagem Vermelho Sangue", viewID: 1550 },
        { id: 31463, name: "Super Drone A1000", viewID: 1561 },
        { id: 31168, name: "Abafadores de Orelha de Carneiro", viewID: 1573 },
        { id: 31167, name: "Orelhas Pretas de Lunático", viewID: 1575 },
        { id: 31186, name: "Gatinho Preto", viewID: 1582 },
        { id: 31187, name: "Laço da Princesa Guerreira", viewID: 1583 },
        { id: 31203, name: "Churrasquelmo", viewID: 1602 },
        { id: 31542, name: "Vaso do Poring Saltitante", viewID: 1634 },
        { id: 31250, name: "Orelhas de Monstrengo", viewID: 1636 },
        { id: 31260, name: "Rastreador Sofisticado", viewID: 1639 },
        { id: 31299, name: "Coelhinho Branco", viewID: 1656 },
        { id: 31482, name: "Cachecol de Lunático", viewID: 1656 },
        { id: 31301, name: "Piscadela", viewID: 1658 },
        { id: 31302, name: "Lacinhos Sombrios", viewID: 1659 },
        { id: 19291, name: "Doge Fofinho", viewID: 1669 },
        { id: 31384, name: "Orelhas de Mentirinha", viewID: 1684 },
        { id: 31398, name: "Piscadela Entediada", viewID: 1693 },
        { id: 31532, name: "Presilha Maravilha", viewID: 1696 },
        { id: 31403, name: "Sinal Japonês", viewID: 1699 },
        { id: 31437, name: "Pequeno Pinguim", viewID: 1705 },
        { id: 31480, name: "Gioia Dorminhoco", viewID: 1705 },
        { id: 31439, name: "Abafadores de Orelha de Coração", viewID: 1707 },
        { id: 31449, name: "Tapa-Olho Floreado", viewID: 1712 },
        { id: 31452, name: "Gata Branca", viewID: 1715 },
        { id: 31538, name: "Aura do Amor", viewID: 1717 },
        { id: 31455, name: "Cabeça de Doge", viewID: 1718 },
        { id: 31472, name: "Asinhas Floridas", viewID: 1723 },
        { id: 31488, name: "Balão de MVP", viewID: 1738 },
        { id: 31491, name: "Gata Lasanhinha", viewID: 1741 },
        { id: 31512, name: "Coelhinho Malhado", viewID: 1754 },
        { id: 31568, name: "Espíritos Taiji", viewID: 1760 },
        { id: 31567, name: "Chifres de Ovelhinha", viewID: 1783 },
        { id: 31574, name: "Comunicador Cibernético", viewID: 1790 },
        { id: 31600, name: "Doge Branquinho", viewID: 1804 },
        { id: 31601, name: "Óculos Modernos", viewID: 1805 },
        { id: 31814, name: "Balões Lunáticos", viewID: 1809 },
        { id: 31614, name: "Camarada Fox", viewID: 1812 },
        { id: 31617, name: "Pelúcia de Lady Tanee", viewID: 1815 },
        { id: 31618, name: "Borboletas Dançantes", viewID: 1816 },
        { id: 31620, name: "Raposa Glacial", viewID: 1818 },
        { id: 31911, name: "Jardim Miniatura", viewID: 1830 },
        { id: 31673, name: "Cestinha de Piquenique", viewID: 1867 },
        { id: 21202, name: "Porquinho", viewID: 1869 },
        { id: 31686, name: "Lobo Filhote", viewID: 1875 },
        { id: 31687, name: "Bolsa do Alquimista", viewID: 1876 },
        { id: 31688, name: "Poring de Bolso", viewID: 1877 },
        { id: 31699, name: "Olhos Felizes", viewID: 1880 },
        { id: 31813, name: "Lunático Simpático", viewID: 1881 },
        { id: 31715, name: "Coelho Cenourinha", viewID: 1887 },
        { id: 31716, name: "Pupilas Carmesins", viewID: 1888 },
        { id: 31946, name: "Olhos Furiosos", viewID: 1897 },
        { id: 31947, name: "Chifres Rochosos", viewID: 1898 },
        { id: 31787, name: "Porquinho de Ombro", viewID: 1915 },
        { id: 31798, name: "Panda Companheiro", viewID: 1922 },
        { id: 31823, name: "Disfarce Irreconhecível", viewID: 1933 },
        { id: 31847, name: "Pupilas Azuladas", viewID: 1945 },
        { id: 31851, name: "Escudo Quântico", viewID: 1949 },
        { id: 31923, name: "Bebê Polar", viewID: 1994 },
        { id: 31924, name: "Pupilas Cerúleas", viewID: 1995 },
        { id: 410005, name: "Aparato Flutuante", viewID: 1996 },
        { id: 31930, name: "Microfone das Estrelas", viewID: 2000 },
        { id: 31931, name: "Lentes Intelectuais", viewID: 2001 },
        { id: 31934, name: "Pupilas Púrpuras", viewID: 2004 },
        { id: 420016, name: "Espíritos de Papel", viewID: 2025 },
        { id: 410030, name: "Trancinhas Azuis", viewID: 2039 },
        { id: 410031, name: "Trancinhas Vermelhas", viewID: 2040 },
        { id: 410032, name: "Trancinhas Amarelas", viewID: 2041 },
        { id: 410033, name: "Trancinhas Verdes", viewID: 2042 },
        { id: 410034, name: "Trancinhas Pretas", viewID: 2043 },
        { id: 410035, name: "Trancinhas Brancas", viewID: 2044 },
        { id: 410036, name: "Trancinhas Marrons", viewID: 2045 },
        { id: 410037, name: "Trancinhas Roxas", viewID: 2046 },
        { id: 410038, name: "Trançado Azulado", viewID: 2047 },
        { id: 410039, name: "Trançado Avermelhado", viewID: 2048 },
        { id: 410040, name: "Trançado Amarelado", viewID: 2049 },
        { id: 410041, name: "Trançado Esverdejado", viewID: 2050 },
        { id: 410042, name: "Trançado Escurecido", viewID: 2051 },
        { id: 410043, name: "Trançado Branquinho", viewID: 2052 },
        { id: 410044, name: "Trançado Bronzeado", viewID: 2053 },
        { id: 410045, name: "Trançado Roxinho", viewID: 2054 },
        { id: 410029, name: "Cesta de Maravilhas", viewID: 2055 },
        { id: 410048, name: "Tigre Companheiro", viewID: 2058 },
        { id: 410049, name: "Pupilas Douradas", viewID: 2060 },
        { id: 21207, name: "Máscara de Minorous", viewID: 2078 },
        { id: 410055, name: "Sombrinha Florida", viewID: 2082 },
        { id: 410054, name: "Laçarote Gigantesco", viewID: 2083 },
        { id: 15877, name: "Presilha Sakura Festiva", viewID: 2085 },
        { id: 410056, name: "Patinho Bonito", viewID: 2086 },
        { id: 410060, name: "Aura de Morceguinhos", viewID: 2093 },
        { id: 410061, name: "Avental de Deviruchi", viewID: 2095 },
        { id: 410063, name: "Laços Docinhos", viewID: 2112 },
        { id: 410068, name: "Banquinha Marinha", viewID: 2126 },
        { id: 410072, name: "Drones Vigilantes", viewID: 2127 },
        { id: 410081, name: "Aura Rochosa", viewID: 2136 },
        { id: 410082, name: "Balões de Aniversário", viewID: 2137 },
        { id: 410095, name: "Angorá de Ombro", viewID: 2151 },
        { id: 410099, name: "Bandagem Possuída", viewID: 2156 },
        { id: 410108, name: "Filhote Shiba Inu", viewID: 2169 },
        { id: 410103, name: "Capacete de Ataduras Vermelhas", viewID: 2171 },
        { id: 410111, name: "Mecha Azul", viewID: 2182 },
        { id: 410112, name: "Mecha Vermelha", viewID: 2183 },
        { id: 410113, name: "Mecha Loira", viewID: 2184 },
        { id: 410114, name: "Mecha Verde", viewID: 2185 },
        { id: 410115, name: "Mecha Castanho Escuro", viewID: 2186 },
        { id: 410116, name: "Mecha Branca", viewID: 2187 },
        { id: 410117, name: "Mecha Castanho Claro", viewID: 2188 },
        { id: 410118, name: "Mecha Lilás", viewID: 2189 },
        { id: 410121, name: "Meda Elmo", viewID: 2199 },
        { id: 410122, name: "Piscadela Rosa", viewID: 2201 },
        { id: 410133, name: "Cookie & Biju", viewID: 2246 },
        { id: 410160, name: "Globo Celestial", viewID: 2265 },
        { id: 410182, name: "Chapéu de Lanterna do Viajante", viewID: 2280 },
        { id: 410198, name: "Devirugangue", viewID: 2299 },
        { id: 410199, name: "Vela da Meia-Noite", viewID: 2301 },
        { id: 19603, name: "Óculos Invisíveis", viewID: 0 },
        { id: 19918, name: "Máscara de Lude", viewID: 0 },
        { id: 20209, name: "Bolhas de Sabão", viewID: 0 },
        { id: 20404, name: "Benção Angelingal", viewID: 0 },
        { id: 20439, name: "Aura Solar", viewID: 0 },
        { id: 31089, name: "Fúria dos Shuras", viewID: 0 },
        { id: 31313, name: "Asas do Anjo Renegado", viewID: 0 },
        { id: 31391, name: "Cristal Exuberante", viewID: 0 },
        { id: 31942, name: "Rosas Românticas", viewID: 0 },
        { id: 410051, name: "Mini Geada", viewID: 0 },
        { id: 31515, name: "Gatinho Curioso", viewID: 0 },
        { id: 410127, name: "Holofote", viewID: 0 },
      ],
      active: false,
    };
  },
  methods: {
    ...mapMutations([
      "SAVE_HEADGEAR_MID",
      "SAVE_HEADGEAR_MID_ID",
      "SAVE_HEADGEAR_MID_NAME",
    ]),
    clickItem: function (event) {
      this.SAVE_HEADGEAR_MID(parseInt(event.target.getAttribute("viewID")));
      this.SAVE_HEADGEAR_MID_ID(parseInt(event.target.getAttribute("id")));
      this.SAVE_HEADGEAR_MID_NAME(event.target.getAttribute("name"));
    },
  },
};
</script>

<style scoped>
.ul-item-list {
  list-style: none;
  padding-top: 2px;
  padding-left: 1rem;
}

.li-item {
  float: left;
  width: 32px;
  height: 32px;
  background: url("~@/assets/img/interface/item-bg.png");
}

.img-item {
  width: 24px;
  height: 24px;
  display: block;
  margin-left: auto;
  margin-right: auto;
}

.item-selected {
  outline: 2px dashed #0d6efd;
  border-radius: 5px;
  filter: contrast(105%) brightness(110%);
}

.item-disabled {
  opacity: 0.5;
  background: url("~@/assets/img/interface/forbidden_item.png");
}
</style>
