<script>
  import { onMount } from "svelte";

  const timeHeaders = [
    "08:10 - 08:50",
    "09:00 - 09:40",
    "09:50 - 10:30",
    "10:40 - 11:20",
    "11:30 - 12:10",
    "12:55 - 13:35",
    "13:50 - 14:30",
    "14:40 - 15:20",
  ];

  const lessons = [
    [
      "Matematik",
      "Matematik",
      "Edebiyat",
      "Arapça",
      "Arapça",
      "Kuran",
      "İngilizce",
      "İngilizce",
    ],
    [
      "Sağlık",
      "Arapça",
      "Arapça",
      "Edebiyat",
      "Edebiyat",
      "Kuran",
      "Kuran",
      "Fizik",
    ],
    [
      "Rehberlik",
      "Tarih",
      "İngilizce",
      "Biyoloji",
      "Kimya",
      "Kimya",
      "Coğrafya",
      "Coğrafya",
    ],
    [
      "Din",
      "Biyoloji",
      "Matematik",
      "Matematik",
      "İngilizce",
      "İngilizce",
      "Kuran",
      "Kuran",
    ],
    [
      "Edebiyat",
      "Edebiyat",
      "Fizik",
      "Tarih",
      "Beden",
      "Beden",
      "Matematik",
      "Matematik",
    ],
  ];

  function getWeekDays(locale) {
    let baseDate = new Date(Date.UTC(2017, 0, 2)); // just a Monday
    let weekDays = [];
    for (let i = 0; i < 5; i++) {
      weekDays.push(baseDate.toLocaleDateString(locale, { weekday: "long" }));
      baseDate.setDate(baseDate.getDate() + 1);
    }
    return weekDays;
  }

  function getCurrentLesson() {
    let d = new Date();
    let time = d.getHours() * 60 + d.getMinutes();

    if (490 <= time && time <= 530) {
      return 0;
    } else if (540 <= time && time <= 580) {
      return 1;
    } else if (590 <= time && time <= 630) {
      return 2;
    } else if (640 <= time && time <= 680) {
      return 3;
    } else if (690 <= time && time <= 730) {
      return 4;
    } else if (780 <= time && time <= 820) {
      return 5;
    } else if (830 <= time && time <= 870) {
      return 6;
    } else if (880 <= time && time <= 920) {
      return 7;
    } else {
      return 32;
    }
  }

  let weekDays = getWeekDays("tr-TR");
  let currentDay = new Date().getDay() - 1;
  let currentLesson = getCurrentLesson();

  onMount(() => {
    const interval = setInterval(() => {
      currentLesson = getCurrentLesson();
    }, 1000);
  });
</script>

<h1>
  {#if -1 < currentDay && currentDay < 6 && currentLesson !== 32}
    Ders {lessons[currentDay][currentLesson]}
  {:else}
    Ders yok
  {/if}
</h1>
<table class="myTable">
  <thead>
    <tr>
      <th>Zaman</th>
      {#each weekDays as weekDay, i}
        {#if i == currentDay}
          <th class="currentDay">{weekDay}</th>
        {:else}
          <th>{weekDay}</th>
        {/if}
      {/each}
    </tr>
  </thead>
  <tbody>
    {#each timeHeaders as header, timeIndex}
      <tr>
        <td>{header}</td>
        {#each lessons as lesson, dayIndex}
          {#if timeIndex == currentLesson && dayIndex == currentDay}
            <td class="currentLesson">{lesson[timeIndex]}</td>
          {:else}
            <td>{lesson[timeIndex]}</td>
          {/if}
        {/each}
      </tr>
    {/each}
  </tbody>
</table>

<style>
  h1 {
    color: #000000;
    font-family: Arial, sans-serif;
    font-size: 3em;
    font-weight: 100;
  }

  .myTable {
    width: 100%;
    margin: auto;
    background-color: #eeeeee;
    border-collapse: collapse;
    border-width: 3px;
    border-color: #71dfe7;
    border-style: solid;
    color: #000000;
  }

  .myTable td,
  .myTable th {
    border-width: 2px;
    border-color: #71dfe7;
    border-style: solid;
    padding: 3px;
    width: 15%;
  }

  .myTable thead {
    background-color: #71dfe7;
  }

  .currentDay {
    color: rgb(255, 255, 255);
    background-color: #1d89e2;
  }

  .currentLesson {
    color: rgb(255, 255, 255);
    background-color: #ff1100;
  }

  @media only screen and (max-width: 600px) {
    h1 {
      font-size: 1.6em;
    }
    .myTable td,
    .myTable th {
      font-size: 3vw;
    }
  }
</style>
