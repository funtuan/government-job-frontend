<template>
  <div class="page">
    <div class="checkbox-all">
      <template v-for="(groupCity, i) in groupCitys">
        <div class="group" :key="i">
          <div class="group-name">
           {{ groupCity.groupName }}
          </div>
          <div class="checkbox-list">
            <template v-for="(city, i) in groupCity.citys">
              <vs-checkbox :key="i" :val="city" v-model="filterCitys">
                {{ city }}
              </vs-checkbox>
            </template>
          </div>
        </div>
      </template>
      <template v-for="(groupSysnam, i) in groupSysnams">
        
        <div class="group" :key="i">
          <div class="group-name">
           {{ groupSysnam.groupName }}
          </div>
          <div class="checkbox-list">
            <template v-for="(sysnam, i) in groupSysnam.sysnams">
              <vs-checkbox :key="i" :val="sysnam" v-model="filterSysnams">
                {{ sysnam }}
              </vs-checkbox>
            </template>
          </div>
        </div>
      </template>
    </div>
    <div class="options">
      <div class="filter-handicap">
        <vs-switch v-model="filterHandicap">
          <template #off>
              含身心障礙職缺
          </template>
          <template #on>
              已排除身心障礙職缺
          </template>
        </vs-switch>
      </div>
      <div class="filter-job-type">
        <vs-select
          placeholder="請選擇官職等"
          v-model="filterJobType"
        >
          <template v-for="(jobType, i) in jobTypes">
            <vs-option :key="i" :value="jobType" :label="jobType">
              {{ jobType }}
            </vs-option>
          </template>
        </vs-select>
      </div>
    </div>
    <div class="notify">
      <div class="notify-button">
        <vs-button
          success
          :active="active == 0"
          @click="autoNotify"
        >
          設置每日自動 LINE 提醒新職缺
        </vs-button>
      </div>
      <div class="notify-detail">
        將套用您的篩選條件，每日下午六點自動通知您新職缺。
      </div>
      <div class="notify-hint">
        若要解除綁定，請至 <a href="https://notify-bot.line.me/my/">https://notify-bot.line.me/my/</a>
      </div>
    </div>
    <div class="list">
      <template v-for="(one, i) in list">
        <a :href="one.fields.view_url" target="_blank" :key="i">
          <vs-card class="card">
            <template #title>
              <div class="card-head">
                {{ one.fields.date_from }} ~ {{ one.fields.date_to }}
              </div>
              <div class="card-title">
                {{ one.fields.org_name }} - {{ one.fields.sysnam }} {{ one.fields.title }} ({{ one.fields.rank_from }} ~ {{ one.fields.rank_to }})
              </div>
              <div class="card-subtitle">
                {{ one.fields.work_addr }}
              </div>
            </template>
            <template #text>
              <p>
                {{ one.fields.work_item }}
              </p>
            </template>
          </vs-card>
        </a>
      </template>
    </div>
  </div>
</template>

<style>
a {
  text-decoration: none;
  color: #000;

}
.page {
  margin: 0 auto;
  max-width: 600px;
  margin-bottom: 80px;
  padding-left: 5px;
  padding-right: 5px;
}

.list {
  margin-top: 20px;
}

.group {
  margin-bottom: 30px;
}

.group-name {
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 10px;
  text-align: left;
}

.checkbox-list {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 20px;
}

.options {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

.card {
  padding-top: 30px;
  text-align: left;
}

.card-head {
  font-size: 12px;
}

.card-title {
  font-size: 20px;
  font-weight: bold;
  padding-top: 6px;
}

.card-subtitle {
  font-size: 14px;
  padding-top: 6px;
}

.vs-card {
  max-width: 100%;
}

.notify {
  margin-top: 40px;
}

.notify-button {
  display: flex;
  justify-content: center;
}

.notify-detail {
  font-size: 12px;
  margin-top: 10px;
  text-align: center;
}

.notify-hint {
  font-size: 12px;
  margin-top: 10px;
  text-align: center;
  color: #999;
}


</style>

<script>
  import axios from "axios";
  export default {
    data:() => ({
      jobTypes: [
        '全部',
        '簡任',
        '薦任',
        '委任',
      ],
      filterHandicap: true,
      filterSysnams: [
        '綜合行政',
        '文教行政',
      ],
      filterCitys: [],
      filterJobType: '薦任',
      groupCitys: [
        {
          groupName: '北區',
          citys: [
            '臺北市',
            '新北市',
            '基隆市',
            '桃園市',
            '新竹市',
            '新竹縣',
            '宜蘭縣',
          ],
        },
        {
          groupName: '中區',
          citys: [
            '臺中市',
            '苗栗縣',
            '彰化縣',
            '南投縣',
          ],
        },
        {
          groupName: '南區',
          citys: [
            '臺南市',
            '高雄市',
            '嘉義市',
            '嘉義縣',
            '屏東縣',
          ],
        },
        {
          groupName: '東區/離島',
          citys: [
            '花蓮縣',
            '臺東縣',
            '澎湖縣',
            '金門縣',
            '連江縣',
          ],
        },
      ],
      groupSysnams: [
        {
          groupName: '行政類',
          sysnams: [
            '綜合行政',
            '人事行政',
            '經建行政',
            '地政',
            '文教行政',
            '社勞行政',
            '會計審計',
            '社會工作',
            '法制',
            '衛生行政',
            '新聞傳播',
            '交通行政',
            '司法行政',
            '環保行政',
            '廉政',
          ]
        },
        {
          groupName: '技術類',
          sysnams: [
            '土木工程',
            '電機工程',
            '資訊處理',
            '獸醫',
            '衛生技術',
            '財稅金融',
            '交通技術',
            '建築工程',
            '圖書史料檔案',
            '機械工程',
            '職業安全衛生',
            '農業技術',
            '工業工程',
            '景觀設計',
            '測量製圖',
            '環資技術',
            '自然保育',
            '都市計畫',
            '水產技術',
            '汽車駕駛',
            '消防技術',
            '藥事',
          ]
        }
      ],
      list: [],
    }),
    methods: {
      // curl -X POST -H "Content-Type: application/json" -d '{"start": 0, "limit": 10, "condition": {"sysnams": ["綜合行政", "文教行政"]}}' http://localhost:8787/
      async refreshList() {
        // 設置 localStorage 紀錄篩選條件
        localStorage.setItem('filters', JSON.stringify({
          filterHandicap: this.filterHandicap,
          filterSysnams: this.filterSysnams,
          filterCitys: this.filterCitys,
          filterJobType: this.filterJobType,
        }))
        const res = await axios.post(process.env.VUE_APP_BACKEND_HOST, {
          start: 0,
          limit: 100,
          condition: {
            sysnams: this.filterSysnams.length ? this.filterSysnams : undefined,
            jobType: this.filterJobType !== '全部' ? this.filterJobType : undefined,
            isDisability: this.filterHandicap ? false : undefined,
            citys: this.filterCitys.length ? this.filterCitys : undefined,
          }
        })
        this.list = res.data;
      },

      // oauth line notify
      async autoNotify() {
        const authEndpoint = 'https://notify-bot.line.me/oauth/authorize';

        const params = new URLSearchParams();
        params.append('response_type', 'code');
        params.append('client_id', process.env.VUE_APP_LINE_NOTIFY_CLIENT_ID);
        params.append('redirect_uri', window.location.origin + '/callback');
        params.append('scope', 'notify');
        params.append('state', JSON.stringify({
          condition: {
            sysnams: this.filterSysnams.length ? this.filterSysnams : undefined,
            jobType: this.filterJobType !== '全部' ? this.filterJobType : undefined,
            isDisability: this.filterHandicap ? false : undefined,
            citys: this.filterCitys.length ? this.filterCitys : undefined,
          },
        }));

        window.location.href = authEndpoint + '?' + params.toString();
      }
    },
    mounted() {
      // 取得 localStorage 紀錄篩選條件
      const filters = JSON.parse(localStorage.getItem('filters')) || {
        filterHandicap: true,
        filterSysnams: [
          '綜合行政',
          '文教行政',
        ],
        filterCitys: [],
        filterJobType: '薦任',
      }
      this.filterHandicap = filters.filterHandicap;
      this.filterSysnams = filters.filterSysnams;
      this.filterCitys = filters.filterCitys;
      this.filterJobType = filters.filterJobType;
      this.refreshList();
    },
    watch: {
      filterSysnams() {
        this.refreshList();
      },
      filterJobType() {
        this.refreshList();
      },
      filterHandicap() {
        this.refreshList();
      },
      filterCitys() {
        this.refreshList();
      }
    }
  }
</script>