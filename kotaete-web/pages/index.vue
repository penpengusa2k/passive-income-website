<template>
  <div>
    <div class="text-center">
      <img src="/site-title.png" alt="KOTAETE" class="h-16 sm:h-20 mb-4 animate-fade-in-down-logo mx-auto block">
      <p class="mt-3 text-lg sm:text-xl text-gray-600 animate-fade-in-up-text">
        あなたの「知りたい」に、みんなの応えを。<br/>
        KOTAETEは簡単・無料のアンケート作成サービスです。
      </p>
      <div class="mt-10 sm:mt-12 text-center">
        <NuxtLink to="/create" class="inline-flex items-center justify-center px-6 py-3 sm:px-8 sm:py-4 border border-transparent text-sm sm:text-base font-medium rounded-full shadow-lg text-white bg-gradient-to-r from-blue-500 to-purple-600 hover:from-blue-600 hover:to-purple-700 transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 animate-subtle-bounce custom-button-width">
          <span class="material-icons-outlined mr-2">add_circle_outline</span>
          さっそくKOTAETEを試してみる
        </NuxtLink>
      </div>
    </div>

    <div class="mt-10 sm:mt-16 text-center animate-section-fade-in">
      <h2 class="text-3xl sm:text-4xl font-bold text-gray-800 mb-8">KOTAETEの使い方</h2>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        <div class="p-6 bg-white rounded-lg shadow-md animate-card-fade-in delay-1">
          <div class="text-blue-600 text-5xl mb-4">1</div>
          <h3 class="text-xl font-semibold text-gray-900 mb-2">KOTAETEを作成</h3>
          <p class="text-gray-700">タイトルと質問を入力するだけで、簡単にあなたのKOTAETE（アンケート）が完成します。</p>
        </div>
        <div class="p-6 bg-white rounded-lg shadow-md animate-card-fade-in delay-2">
          <div class="text-blue-600 text-5xl mb-4">2</div>
          <h3 class="text-xl font-semibold text-gray-900 mb-2">URLをシェア</h3>
          <p class="text-gray-700">作成された専用URLをSNSやメールで共有。あっという間に回答が集まります。</p>
        </div>
        <div class="p-6 bg-white rounded-lg shadow-md animate-card-fade-in delay-3">
          <div class="text-blue-600 text-5xl mb-4">3</div>
          <h3 class="text-xl font-semibold text-gray-900 mb-2">結果を確認・分析</h3>
          <p class="text-gray-700">集まった回答はリアルタイムでグラフ化。CSVダウンロードで詳細な分析も可能です。</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
// 必要であればここにスクリプトを追加
</script>

<style scoped>
/* ロゴのフェードイン */
@keyframes fadeInDownLogo {
  from { opacity: 0; transform: translateY(-20px); }
  to { opacity: 1; transform: translateY(0); }
}
.animate-fade-in-down-logo {
  opacity: 0; /* 初期状態を非表示に設定 */
  animation: fadeInDownLogo 0.8s ease-out forwards; /* 1s -> 0.8s */
}

/* 説明文のフェードイン */
@keyframes fadeInUpText {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}
.animate-fade-in-up-text {
  opacity: 0; /* 初期状態を非表示に設定 */
  animation: fadeInUpText 1s ease-out forwards 0.2s; /* 1.2s -> 1s, 0.3s -> 0.2s */
}

/* ボタンの控えめなバウンス */
@keyframes subtleBounce {
  0%, 100% { transform: translateY(0); }
  20% { transform: translateY(-3px); }
  40% { transform: translateY(0); }
  60% { transform: translateY(-1px); }
  80% { transform: translateY(0); }
}
.animate-subtle-bounce {
  animation: subtleBounce 1s ease-out 0.6s 1 forwards; /* 0.8s -> 0.6s */
}

/* KOTAETEの使い方セクション全体を遅延フェードイン */
@keyframes sectionFadeIn {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}
.animate-section-fade-in {
  opacity: 0; /* 初期状態を非表示に設定 */
  animation: sectionFadeIn 1s ease-out forwards 1.2s; /* 1.5s -> 1s, 1.8s -> 1.2s */
}

/* 各カードのフェードイン */
@keyframes cardFadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}
.animate-card-fade-in {
  opacity: 0; /* 初期状態では非表示 */
  animation: cardFadeIn 0.6s ease-out forwards; /* 0.8s -> 0.6s */
}

/* カードごとの遅延設定 */
.animate-card-fade-in.delay-1 { animation-delay: 1.5s; } /* 2.3s -> 1.2s (sectionFadeInの終了) + 0.3s */
.animate-card-fade-in.delay-2 { animation-delay: 1.7s; } /* 1.5s + 0.2s */
.animate-card-fade-in.delay-3 { animation-delay: 1.9s; } /* 1.7s + 0.2s */

/* ボタンの初期幅を固定してリサイズを防ぐ */
.custom-button-width {
  min-width: 280px; /* ここを調整して、ボタンの文字が収まる適切な幅を設定してください */
}
/* smブレイクポイントでのボタンの幅調整 */
@media (min-width: 640px) { /* TailwindCSSのsmブレイクポイント */
  .custom-button-width {
    min-width: 320px; /* smサイズ以上での幅を調整してください */
  }
}
</style>
