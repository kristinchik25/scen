### Схема автоматизации техподдержки DeepFocus

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 
  'primaryColor': '#ffffff', 
  'primaryBorderColor': '#000000', 
  'primaryTextColor': '#000000',
  'secondaryColor': '#ffffff', 
  'secondaryBorderColor': '#000000', 
  'secondaryTextColor': '#000000',
  'tertiaryColor': '#ffffff', 
  'tertiaryBorderColor': '#000000', 
  'tertiaryTextColor': '#000000',
  'lineColor': '#ffffff', 
  'textColor': '#000000',
  'edgeLabelBackground': '#ffffff',
  'fontSize': '14px',
  'background': '#24292e'
}}}%%

graph TD
    START[НАЧАЛО: Клиент обращается в поддержку] --> CLASSIFIER[AI-КЛАССИФИКАТОР: Анализ категории и критичности]
    
    CLASSIFIER --> CRITICAL{Проблема критическая?}
    
    CRITICAL -->|ДА| TICKET_P0[Создать тикет P0: Уведомить инженера, SLA: 15 мин]
    CRITICAL -->|НЕТ| VIP{Тариф VIP?}
    
    VIP -->|ДА| PRIORITY[Приоритетная очередь: Уведомить менеджера]
    VIP -->|НЕТ| STANDARD[Стандартная очередь]
    
    TICKET_P0 --> RESOLVE
    PRIORITY --> RESOLVE{AI может решить автоматически?}
    STANDARD --> RESOLVE
    
    RESOLVE -->|ДА| AUTO[AUTO-RESOLVE: Отправить инструкцию]
    RESOLVE -->|НЕТ| HUMAN[Передать человеку: Создать тикет + логи]
    
    AUTO --> HELPED{Помогло?}
    HELPED -->|ДА| CLOSE1[Закрыть тикет: Записать в Sheets]
    HELPED -->|НЕТ| HUMAN
    
    HUMAN --> SOLVED[Проблема решена]
    SOLVED --> RATE[Оценка клиента]
    CLOSE1 --> RATE
    
    RATE --> SCORE{Оценка?}
    SCORE -->|≥ 9| PROMO[Отправить просьбу оставить отзыв]
    SCORE -->|≤ 6| QUALITY[Создать тикет в CRM: Уведомить службу качества]
    SCORE -->|7-8| CLOSE2[Закрыть т
