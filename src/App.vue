<template>
  <Header :header="this.header" />
  <div class="content-container">
    <section class="section-container" id="missions" style="width:435px; height:714px;">
      <div class="section-header clipped-medium-backward">
        <img src="/icons/mission-icon.svg" />
        <h1>Mission Log</h1>
      </div>
      <div class="section-content-container">
        <h3>Current Assignment</h3>
        <Markdown :source="current_md" class="markdown" />
        <h3>Mission List</h3>
        <div class="mission-list-container">
          <Mission
            v-for="item in this.missions"
            :key="item.slug"
            :mission="item"
            :selected="this.mission_slug"
            @click="selectMission(item)"
          />
        </div>
      </div>
    </section>
    <section class="section-container" id="events" style="width:435px; height:714px;">
      <div class="section-header clipped-medium-backward">
        <img src="/icons/events-icon.svg" />
        <h1>Events Log</h1>
      </div>
      <div class="section-content-container">
        <Markdown :source="events" class="markdown" />
      </div>
    </section>
    <section class="section-container" id="pilots" style="width:894px; height:714px;">
      <div style="height:52px; overflow:hidden;">
        <div class="section-header clipped-medium-backward-pilot">
          <img src="/icons/pilot-icon.svg" />
          <h1>Pilot Roster</h1>
        </div>
        <div class="rhombus-back">&nbsp;</div>
      </div>
      <div class="section-content-container">
        <div class="pilot-list-container">
          <Pilot v-for="item in this.pilots" :key="item.slug" :pilot="item" />
        </div>
      </div>
    </section>
  </div>
  <svg
    style="visibility: hidden; position: absolute;"
    width="0"
    height="0"
    xmlns="http://www.w3.org/2000/svg"
    version="1.1"
  >
    <defs>
      <filter id="round">
        <feGaussianBlur in="SourceGraphic" stdDeviation="5" result="blur" />
        <feColorMatrix
          in="blur"
          mode="matrix"
          values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 19 -5"
          result="goo"
        />
        <feComposite in="SourceGraphic" in2="goo" operator="atop" />
      </filter>
    </defs>
  </svg>
  <audio autoplay>
    <source src="/startup.ogg" type="audio/ogg" />
  </audio>
  <Footer/>
</template>

<script>
import Header from './components/layout/Header.vue';
import Footer from './components/layout/Footer.vue';
import Mission from './components/Mission.vue';
import Pilot from './components/Pilot.vue';
import Markdown from 'vue3-markdown-it';

export default {
  components: {
    Header,
    Footer,
    Mission,
    Pilot,
    Markdown
  },

  data() {
    return {
      "mission_slug": "001",
      "current_md": "",
      "events": "",
      "missions": [
        {
          "slug": "001",
          "name": "새로운 피",
          "status": "start"
        },
      ],
      "pilots": [
        {
          "callsign": "GOLDEN HOUR",
          "alias": "빅터 맥스웰 지킬",
          "code": "567158be-1qf5-49c2-77s7-ccf3a5975a96///GMS-MER-HAVENS-RING//NTY3MTU4YmUtMXFmNS00OWMyLTc3czctY2NmM2E1OTc1YTk2",
          "corpro": "GMS",
          "frame": "SAGARMATHA",
          "mech": "SURGERY"
        },
        {
          "callsign": "Kensei",
          "alias": '텐류 츠루기',
          "code": "d84526262e-d87e-4e10-99c8-df011qcc4867///GMS-MER-HAVENS-RING//ZDg0NTI2MjYyZS1kODdlLTRlMTAtOTljOC1kZjAxMXFjYzQ4Njc=",
          "corpro": "GMS",
          "frame": "EVEREST",
          "mech": "SEN RYU"
        },
        {
          "callsign": "Hound",
          "alias": '하티',
          "code": "678dc392&is=678c7212&hm=325a8bdc4d8f///GMS-MER-HAVENS-RING//Njc4ZGMzOTImaXM9Njc4YzcyMTImaG09MzI1YThiZGM0ZDhm",
          "corpro": "GMS",
          "frame": "EVEREST",
          "mech": "Fenrir"
        },
        {
          "callsign": "Old man",
          "alias": '도노반 오스틴',
          "code": "d456o-7n57-57-b76a-asd9n44o-00s4ti-75n///GMS-MER-HAVENS-RING//ZDQ1Nm8tN241Ny01Ny1iNzZhOW40NG8tMDBzNHRpLTc1bg==",
          "corpro": "GMS",
          "frame": "EVEREST",
          "mech": "metalcoffin"
        },
        {
          "callsign": "Friday",
          "alias": '드라이젠',
          "code": "6b09015a-c027-4130-a335-15a0142b6c07///GMS-MER-HAVENS-RING//NmIwOTAxNWEtYzAyNy00MTMwLWEzMzUtMTVhMDE0MmI2YzA3",
          "corpro": "GMS",
          "frame": "EVEREST",
          "mech": "MICHAEL"
        },
        {
          "callsign": "Winter",
          "alias": '에페스',
          "code": "6b09015a-c027-4130-a335-15a0142b6c07///GMS-MER-HAVENS-RING//NmIwOTAxNWEtYzAyNy00MTMwLWEzMzUtMTVhMDE0MmI2YzA3",
          "corpro": "GMS",
          "frame": "CHOMOLUNGMA",
          "mech": "Schneewittchen"
        },
        {
          "callsign": "BAZZ",
          "alias": '카코파푸카',
          "code": "a15a01-c02742b6c07-4130-a335-6b09015///GMS-MER-HAVENS-RING//YTE1YTAxLWMwMjc0MmI2YzA3LTQxMzAtYTMzNS02YjA5MDE1",
          "corpro": "GMS",
          "frame": "EVEREST",
          "mech": "KORAN"
        },
      ],
      "header": {
        "planet": "Genesis-15",
        "year": "5014u",
        "system": "Noah-8",
        "gate": "Atlas-Yuno",
        "ring": "Atlas-151",
        "headerTitle": "HEAVENS RING",
        "headerSubtitle": "Mercenary Company",
        "subheaderTitle": "General Massive Briefing Systems",
        "subheaderSubtitle": "Online",
      },
      "options":{
        "eventsMarkdownPerMission": true
      }
    }
  },

  created() {
    this.loadMissionMarkdown()
    this.loadEventsMarkdown()
  },

  computed: {

  },

  methods: {
    selectMission(mission) {
      this.mission_slug = mission.slug;
      this.loadMissionMarkdown()
      if(this.options.eventsMarkdownPerMission){
        this.loadEventsMarkdown();
      }
    },
    loadMissionMarkdown() {
      let self = this;
      let md = `/missions/${self.mission_slug}.md`
      var client = new XMLHttpRequest();
      client.open('GET', md);
      client.onreadystatechange = function () {
        self.current_md = client.responseText;
      }
      client.send();
    },
    loadEventsMarkdown() {
      let self = this;
      let md = "";

      if(self.options.eventsMarkdownPerMission){
        md = `/events/${self.mission_slug}.md`
      }
      else {
        md = "/events.md"
      }

      var client = new XMLHttpRequest();
      client.open('GET', md);
      client.onreadystatechange = function () {
        self.events = client.responseText;
      }
      client.send();
    }
  }

}
</script>


<style lang="scss">
#app {
  width: 1902px;
  height: 910px;
  overflow: hidden;
}
</style>
