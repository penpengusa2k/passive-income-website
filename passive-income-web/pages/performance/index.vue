<template>
  <div class="container mx-auto px-4 py-8">
    <h1 class="text-4xl md:text-5xl font-extrabold text-neutral-darkest dark:text-neutral-lightest mb-4">実績とデータ</h1>
    <p class="text-lg text-neutral-darkest/80 dark:text-neutral-light/80 mb-10">
      このサイトの成長記録を、具体的なデータで公開します。
    </p>

    <section class="py-6 mb-12">
      <h2 class="text-3xl font-bold text-center text-neutral-darkest dark:text-neutral-lightest mb-8">サマリー</h2>
      <div class="grid md:grid-cols-3 gap-6 text-center">
        <div class="bg-white dark:bg-neutral-dark rounded-lg shadow-md p-6 border-t-4 border-primary">
          <p class="text-sm text-neutral-darkest font-semibold">開発ツール数</p>
          <p class="text-primary text-5xl font-bold mt-2">0</p>
        </div>
        <div class="bg-white dark:bg-neutral-dark rounded-lg shadow-md p-6 border-t-4 border-secondary">
          <p class="text-sm text-neutral-darkest font-semibold">累計収益</p>
          <p class="text-secondary text-5xl font-bold mt-2">¥{{ totalRevenue.toLocaleString() }}</p>
        </div>
        <div class="bg-white dark:bg-neutral-dark rounded-lg shadow-md p-6 border-t-4 border-accent">
          <p class="text-sm text-neutral-darkest font-semibold">公開記事数</p>
          <p class="text-accent text-5xl font-bold mt-2">{{ totalArticles }}</p>
        </div>
      </div>
    </section>

    <section class="py-6 mb-12">
      <h2 class="text-3xl font-bold text-center text-neutral-darkest dark:text-neutral-lightest mb-8">サイトPV推移</h2>
      <div class="bg-white dark:bg-neutral-dark rounded-lg shadow-md p-4 md:p-6 h-96 flex items-center justify-center">
        <p class="text-neutral-dark dark:text-neutral-light">今後実装予定です。</p>
      </div>
    </section>

    <section class="py-6 mb-12">
      <h2 class="text-3xl font-bold text-center text-neutral-darkest dark:text-neutral-lightest mb-8">収益レポート</h2>
      <div class="bg-white dark:bg-neutral-dark rounded-lg shadow-md p-4 md:p-6 h-96">
        <BarChart v-if="cumulativeRevenueChartData && cumulativeRevenueChartData.datasets && cumulativeRevenueChartData.datasets.length > 0" :data="cumulativeRevenueChartData" :options="chartOptions" />
        <div v-else class="flex items-center justify-center h-full text-neutral-dark dark:text-neutral-light">
          <p>データを読み込み中...</p>
        </div>
      </div>
    </section>

    <section class="py-6">
      <h2 class="text-3xl font-bold text-center text-neutral-darkest dark:text-neutral-lightest mb-8">今後のマイルストーン</h2>
      <div class="prose max-w-none text-neutral-darkest/90 dark:text-neutral-light/90 leading-relaxed text-center mx-auto">
        <p>ITの力を活用した不労所得の実現は、まだ始まったばかりです。今後も新たなツールの開発、コンテンツの拡充、そして収益化手法の最適化に挑戦し続けます。このページのデータが、右肩上がりに成長していく様子にご期待ください。</p>
      </div>
    </section>
  </div>
</template>

<script setup>
import { Line as LineChart, Bar as BarChart } from 'vue-chartjs';
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  LineElement,
  LinearScale,
  CategoryScale,
  PointElement,
  BarElement
} from 'chart.js';

ChartJS.register(
  Title,
  Tooltip,
  Legend,
  LineElement,
  LinearScale,
  CategoryScale,
  PointElement,
  BarElement
);

const config = useRuntimeConfig();


// 累計収益推移のダミーデータ (手動更新)
const cumulativeRevenueChartData = {
  labels: ['2025年6月'],
  datasets: [
    {
      label: '累計収益 (円)',
      backgroundColor: '#34a853',
      data: [0]
    }
  ]
};

const totalRevenue = computed(() => {
  const data = cumulativeRevenueChartData.datasets[0].data;
  // データがある場合は最後の値を返し、ない場合は0を返す
  return data.length > 0 ? data[data.length - 1] : 0;
});

// 取得した記事数をリアクティブなcomputedプロパティで表示
const totalArticles = computed(() => {
  return config.public.articleCount ?? 0; // runtimeConfigから取得
});

// グラフの共通オプション
const chartOptions = {
  responsive: true,
  maintainAspectRatio: false,
  plugins: {
    legend: {
      display: true,
      position: 'top'
    },
    tooltip: {
      mode: 'index',
      intersect: false
    }
  },
  scales: {
    y: {
      beginAtZero: true,
    }
  }
};

useHead({
  title: '実績とデータ',
  meta: [
    { name: 'description', content: 'ITを活用した不労所得構築に関する具体的な実績、データ、そして今後の展望を公開。累計収益とPV推移。' }
  ]
});
</script>

<style scoped>
/* 必要であれば、このページ固有のスタイルをここに記述 */
</style>
