# Таблица переходов

| Исходное состояние | Переходное состояние | Событие |
|--------------------|----------------------|---------|
| Begin | payment_initiated | initiate_payment |
| payment_initiated | amount_blocked | block_amount |
| amount_blocked | fraud_check_pending | send_fraud_check |
| fraud_check_pending | fraud_check_success | fraud_success |
| fraud_check_pending | fraud_check_manual | fraud_send_manual |
| fraud_check_pending | fraud_check_failed | fraud_detected |
| fraud_check_success | payment_executed | execute_payment |
| fraud_check_manual | fraud_check_success | fraud_manual_approved |
| fraud_check_manual | fraud_check_success | fraud_manual_timeout |
| fraud_check_manual | fraud_check_failed | fraud_manual_rejected |
| fraud_check_failed | amount_released | release_amount |
| payment_executed | success_notified | notify_success |
| amount_released | failure_notified | notify_failure |
