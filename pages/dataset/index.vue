<script setup lang="ts">
const slug = useRoute().params.slug;
const { locale } = useI18n();

const { t } = useI18n();

// const item = await queryContent(`/${locale.value}/page/` + "dataset").findOne();

const runtimeConfig = useRuntimeConfig();
const appUrl = runtimeConfig.public.appUrl;

const item = {
  title: "dataset",
  "body": [
    {
        "label": "地名辞書",
        "description": "地名をまとめて利用するためのデータセット",
        "extent": "CSV",
        "download": `${appUrl}/data/index.csv`,
        "_viewer": "/mirador/?manifest=/iiif/main/manifest.json",
        "_": [
            {
                "label": "アノテーション",
                "description": "IIIFマニフェスト",
                "extent": "JSON",
                "download": "/iiif/main/manifest.json",
                "viewer": "/mirador/?manifest=/iiif/main/manifest.json"
            }
        ]
    }
  ]
}

const localePath = useLocalePath();

const bh = [
  {
    title: t("top"),
    disabled: false,
    to: localePath({ name: "index" })
  },
  {
    title: t(item.title),
    disabled: false,
  },
];

const apis = [
  {
    "name": "JSON",
    "description": "JSON形式のデータセット",
    "url": `${appUrl}/api/items/index.json`
  },
  {
    "name": t("sitemap"),
    "description": "サイトマップ",
    "url": `${appUrl}/sitemap.xml`
  },
  {
    "name": t("resourcesync"),
    "description": "ResourceSync",
    "url": `${appUrl}/resourcesync/resourcelist-index.xml`
  }
]
</script>
<template>
  <LayoutsCommon :title="item.title" :items="bh">
    <h1>{{ $t(item.title) }}</h1>

    <v-table>
      <thead>
        <tr>
          <td>{{ $t("name") }}</td>
          <td>{{ $t("description") }}</td>
          <td>{{ $t("format") }}</td>
          <td>{{ $t("download") }}</td>
          <td>{{ $t("viewer") }}</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="row in item.body">
          <td width="20%">
            {{ row.label }}
          </td>
          <td width="20%">
            {{ row.description }}
          </td>
          <td width="20%">
            {{ row.extent }}
          </td>
          <td width="20%">
            <a :href="row.download">
              {{ row.download }}
            </a>
          </td>
          <td width="20%">
            <a :href="row.viewer">
              {{ row.viewer }}
            </a>
          </td>
        </tr>
      </tbody>
    </v-table>

    <v-btn class="mt-10" color="primary" flat :to="localePath({name: 'dictionary'})">地名辞書</v-btn>

    <h2 class="mt-10">{{ "API" }}</h2>

    <v-table>
      <thead>
        <tr>
          <td>{{ $t("name") }}</td>
          <td>{{ $t("description") }}</td>
          <td>{{ $t("url") }}</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="api in apis">
          <td width="20%">
            {{ api.name }}
          </td>
          <td width="40%">
            {{ api.description }}
          </td>
          <td width="40%">
            <a :href="api.url">
              
            {{ api.url }}
            </a>
          </td>
          
        </tr>
      </tbody>
    </v-table>
  </LayoutsCommon>
</template>
