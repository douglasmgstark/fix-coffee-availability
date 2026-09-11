# ☕ The Moccamaster Loop

*One cup. One contribution. Continuous coffee.*

Before taking a cup, complete **the first applicable action**:

1. **Tank empty?** Fill it for the next batch. Your part is done.
2. **Filter or grounds used?** Replace both. Your part is done.
3. **Everything ready, with room for the entire next batch?** Start brewing. Your part is done.

One action per cup. The next person picks up where you left off. Water and coffee can be prepared **even when the pot is full**. If brewing is already running, or everything is ready but the pot is too full, there is nothing to do this time.

> **The last cup is yours only when the next brew is running.**  
> If your one action was preparation, leave the last cup until brewing has started.

```python
# Pseudocode. You are the agent.

def contribute():
    if machine.is_brewing():
        return

    if tank.is_empty():
        tank.fill_for_next_batch()
    elif not basket.is_fresh():
        basket.replace_filter_and_coffee()
    elif pot.free_space() >= tank.batch_volume():
        machine.start_brewing()


def moccamaster_loop(agent):
    if agent is None:
        return  # Everyone has gone home.

    contribute()  # One action. Pass it on.

    last_cup_locked = pot.cups <= 1 and not machine.is_brewing()
    if pot.cups > 0 and not last_cup_locked:
        agent.pour_coffee()

    return moccamaster_loop(next_thirsty_agent())
```

`fallback="Douglas"` has been removed. Please handle your own dependencies.
