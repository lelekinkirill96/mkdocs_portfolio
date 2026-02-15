## Часто задаваемые вопросы о сканировании сети


<script>
function toggleText() {
  const text = document.getElementById("hiddenText");
  const link = document.getElementById("toggleLink");

  if (text.style.display === "none" || text.style.display === "") {
    text.style.display = "block";
    link.textContent = "Скрыть ответ ▼";
  } else {
    text.style.display = "none";
    link.textContent = "Не положит ли сканирование сеть? ▶";
  }
}
</script>

<style>
.toggle-link {
  color: #2c3e50;
  font-weight: 600;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  margin-bottom: 8px;
  text-decoration: none;
  font-size: 16px;
}

.toggle-link:hover {
  color: #3498db;
}

.hidden-text {
  display: none;
  background-color: #fefefe;
  border: 1px solid #e0e0e0;
  border-radius: 6px;
  padding: 16px;
  margin-top: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
  line-height: 1.5;
}

.section-title {
  font-weight: 600;
  color: #2c3e50;
  margin-top: 12px;
  margin-bottom: 8px;
  font-size: 15px;
}

.section-content {
  margin-left: 16px;
  margin-bottom: 12px;
}

.section-content li {
  margin-bottom: 6px;
}
</style>

<a id="toggleLink" class="toggle-link" onclick="toggleText()">
  Не положит ли сканирование сеть? ▶
</a>

<div id="hiddenText" class="hidden-text">
  Сканирование сети не перегрузит инфраструктуру, если правильно настроить параметры:

  <div class="section-title">✅ Ограничение скорости и нагрузки:</div>
  <ul class="section-content">
    <li>Установить максимум параллельных задач (например, 5–10).</li>
    <li>Задать лимиты на количество запросов в секунду (например, 100–500 пакетов/сек).</li>
    <li>Настроить тайм-ауты для неотвечающих хостов (2–5 секунд).</li>
    <li>Ограничить пропускную способность (например, 1–10 Мбит/с).</li>
  </ul>

  <div class="section-title">✅ Щадящие методы сканирования:</div>
  <ul class="section-content">
    <li>Агентное сканирование (минимальная нагрузка на сеть).</li>
    <li>Сканирование с учётными данными (SSH/WinRM/SNMP) вместо массовых сетевых запросов.</li>
  </ul>

  <div class="section-title">✅ Оптимальное время выполнения:</div>
  <ul class="section-content">
    <li>Планировать задачи на непиковые часы (ночь, выходные).</li>
    <li>Использовать технологические окна для критически важных сегментов.</li>
  </ul>

  <div class="section-title">✅ Мониторинг и корректировка:</div>
  <ul class="section-content">
    <li>Следить за загрузкой сети и устройств во время сканирования.</li>
    <li>При превышении порогов — приостанавливать или перенастраивать задачи.</li>
  </ul>
</div>


---

### Как Discovery видит устройства за NAT или в закрытых сегментах?

Для полного покрытия инфраструктуры используйте **комбинацию сенсоров и агентов**. Сенсор подключается к основному серверу Vulns.io и выполняет сканирование от своего имени, передавая результаты обратно.

**Преимущества:**

- Сканирует устройства, недоступные напрямую из основной сети.
  
- Поддерживает все режимы сканирования (агентный, безагентный, "чёрный ящик").
  
- Может быть развёрнут в облаке, DMZ, изолированных VLAN.

---

### Зачем нужен Discovery, если у нас есть актуальный список в Active Directory / CMDB?

Discovery — **не альтернатива, а дополнение** к AD/CMDB. Он помогает:

- Закрыть "слепые зоны" (Shadow IT, неучтённые устройства).
  
- Контролировать актуальность данных.
  
- Обнаруживать устаревшие или новые устройства.
  
- Обеспечивать полноту сканирования на уязвимости.

---

### Как система понимает, что это один и тот же ноутбук, если он сменил IP или перешёл с Wi-Fi на медь?

Система **Vulns.io Enterprise VM** использует **комплекс уникальных идентификаторов** для дедубликации:

- MAC-адрес.

- UUID.

- Имя хоста (hostname).

- Ключи реестра (для Windows).

- Данные инвентаризации и список ПО.

Это позволяет корректно определять устройство даже при смене IP или типа подключения.

---

### Можно ли доверять результатам Discovery, если у половины устройств закрыты порты?

**Без дополнительных мер — нет.** Discovery покажет только "живые" хосты, но не даст полной информации об ОС, ПО и уязвимостях.

**С дополнительными мерами — да.** Используйте:

- Сканирование с учётными данными (SSH/WinRM/SNMP).

- **Port Knocking** для доступа к закрытым портам.

- Сенсоры для сканирования изолированных сегментов.

- Интеграцию с AD/CMDB для дополнения данных.
