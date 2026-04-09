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
    START[Начало: Клиент обращается в поддержку] --> CLASSIFIER[AI-классификатор: Анализ категории и критичности]
    
    CLASSIFIER --> CRITICAL{Проблема критическая?}
    
    CRITICAL -->|ДА| TICKET_P0[Создать тикет P0: Уведомить инженера, SLA 15 мин]
    CRITICAL -->|НЕТ| VIP{Тариф VIP?}
    
    VIP -->|ДА| PRIORITY[Приоритетная очередь: Уведомить менеджера]
    VIP -->|НЕТ| STANDARD[Стандартная очередь]
    
    TICKET_P0 --> RESOLVE
    PRIORITY --> RESOLVE{AI может решить автоматически?}
    STANDARD --> RESOLVE
    
    RESOLVE -->|ДА| AUTO[Auto-resolve: Отправить инструкцию]
    RESOLVE -->|НЕТ| HUMAN[Передать человеку: Создать тикет + логи]
    
    AUTO --> HELPED{Помогло?}
    HELPED -->|ДА| CLOSE1[Закрыть тикет: Записать в Sheets]
    HELPED -->|НЕТ| HUMAN
    
    HUMAN --> SOLVED[Проблема решена]
    SOLVED --> RATE[Оценка клиента]
    CLOSE1 --> RATE
    
    RATE --> SCORE{Оценка?}
    SCORE -->|Оценка >= 9| PROMO[Отправить просьбу оставить отзыв]
    SCORE -->|Оценка <= 6| QUALITY[Создать тикет в CRM: Уведомить службу качества]
    SCORE -->|Оценка 7-8| CLOSE2[Закрыть тикет]
    
    PROMO --> CLOSE2
    QUALITY --> CLOSE2
    
    style START fill:#90EE90,stroke:#000000,color:#000000
    style CLASSIFIER fill:#87CEEB,stroke:#000000,color:#000000
    style CRITICAL fill:#FFB6C1,stroke:#000000,color:#000000
    style VIP fill:#FFD700,stroke:#000000,color:#000000
    style RESOLVE fill:#FFB6C1,stroke:#000000,color:#000000
    style HELPED fill:#FFB6C1,stroke:#000000,color:#000000
    style SCORE fill:#FFB6C1,stroke:#000000,color:#000000
    style AUTO fill:#98FB98,stroke:#000000,color:#000000
    style HUMAN fill:#DDA0DD,stroke:#000000,color:#000000
    style TICKET_P0 fill:#FF6347,stroke:#000000,color:#000000
    style PRIORITY fill:#FFA500,stroke:#000000,color:#000000
    style PROMO fill:#90EE90,stroke:#000000,color:#000000
    style QUALITY fill:#FF6347,stroke:#000000,color:#000000
    style SOLVED fill:#98FB98,stroke:#000000,color:#000000
    style RATE fill:#87CEEB,stroke:#000000,color:#000000
    style CLOSE1 fill:#98FB98,stroke:#000000,color:#000000
    style CLOSE2 fill:#98FB98,stroke:#000000,color:#000000
    style STANDARD fill:#ffffff,stroke:#000000,color:#000000
