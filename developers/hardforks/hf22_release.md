# HF22: Новые возможности

## Система воркеров

О системе воркеров/исполнителей можно прочитать [здесь](https://golos.id/ru--golos/@lex/sistema-vorkerov-dlya-golos-blockchain), этот функционал позволит привлечь пользователей к участию в развитии Golos Blockchain, появлению новых приложений, клиентов, игр, ботов, документации, маркетинговой активности и многому другому.

Важно, что не только делегаты, а все участники сообщества могут голосовать по заявкам воркеров.

## Распределение эмиссии

У делегатов появилась возможность менять параметры % распределения эмиссии по пулам 

* worker\_reward\_percent
* witness\_reward\_percent
* vesting\_reward\_percent 

Также были сняты ограничения по параметрам на % прибыли от делегирования `max_delegated_vesting_interest_rate` \([исключен предел](https://github.com/GolosChain/golos/issues/1008) в макс. 80%\) и кураторских отчислений `min_curation_percent` \([исключен предел](https://github.com/GolosChain/golos/issues/1009) в мин. 25%\). Оба параметра опционально позволят исп. делегатам значения в диапазоне от 0 до 100%. Параметр количества апвоутов в день `vote_regeneration_per_day` сделан голосуемым делегатами \(по умолчанию 10 вместо 40\).

Исправлена и [ошибка](https://github.com/GolosChain/golos/issues/1010) из-за которой пользователи не могли добавлять посты в случае превышения порога активности на публикацию комментариев.

## Понижение СГ при неактивности

В случае если на аккаунте в течении 12 месяцев \(срок голосуемый делегатами `account_idleness_time`\) не было совершенно действий с использованием активного ключа \(перевод токенов, ставка на внутренней бирже, голос за делегата и пр.\) - отменяется делегирование и запускается механизм понижения Силы Голоса в ликвидные токены Голос. 

Тем самым такие аккаунты перестанут влиять на выбор делегатов и получать % на вестинг/СГ из эмиссии при "полной пассивности" участия в проекте.

## Принцип голосования за делегатов

Важным [изменением](https://github.com/GolosChain/golos/issues/820) станет и смена принципа голосования за делегатов. Если ранее можно было выбирать 30 делегатов с полным весом своего стека СГ за каждого из них \(о минусах подобного писали [тут](https://golos.id/newgolos/@newgolos/voterules323289)\), после 22ХФ размер стека СГ стал делиться на кол-во поддерживаемых делегатов. 

Напр. если у вас 30 000 СГ и вы поддержите 3 делегатов, в поддержку каждого из них "пойдет" по 10 000 СГ.

Также в код был добавлен автоматический сброс голосов с делегатов, у которых прошло 12 месяцев \(срок голосуемый делегатами `witness_idleness_time`\) с момента подписания последнего блока.

## Решение по вопросу GBG

С учётом того, что вариант из [поста](https://golos.id/golos/@gusaru/sostoyanie-defolta-golos-blockchain-i-chto-s-etim-delat) @gusaru ранее [рассматривался](https://steemit.com/steem/@dantheman/steem-dollar-stability-enhancements) как оптимальный и одним из создателей Bitshares/Steem/EOS, в составе ХФ была принята именно эта реализация: _при объеме долга более 20% запускается механизм ежедневной конвертации 1% доступных на балансах GBG в GOLOS_ \(ордера на внутренней бирже перед конвертацией будут отменяться\).

Процент ежедневной конвертации `sbd_debt_convert_rate` голосуемый делегатами, по умолчанию 1%. 
