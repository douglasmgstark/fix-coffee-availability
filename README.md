# ☕ The Moccamaster Loop

*Think recursively. Brew proactively.*

Every coffee comes with three checks:

1. **Water ready?** If the tank is empty, fill it for the next batch.
2. **Coffee ready?** If the filter or grounds are used, replace both.
3. **Room to brew?** If the pot can hold the entire next batch, start it.

Prepare the water, filter and coffee **even when the pot is full**. Once brewing starts, let the cycle finish before preparing the next batch. Check again after pouring: your cup may have made room.

> **The last cup is yours only when the next brew is running.**  
> “I was going to” is not a brewing state.

```python
# Pseudocode. You are the agent.

def keep_coffee_ready():
    if machine.is_brewing():
        return

    if tank.is_empty():
        tank.fill_for_next_batch()
    if not basket.is_fresh():
        basket.replace_filter_and_coffee()
    if pot.free_space() >= tank.batch_volume():
        machine.start_brewing()


def moccamaster_loop(agent):
    if agent is None:
        return  # Everyone has gone home.

    keep_coffee_ready()

    last_cup_locked = pot.cups <= 1 and not machine.is_brewing()
    if pot.cups > 0 and not last_cup_locked:
        agent.pour_coffee()
        keep_coffee_ready()

    return moccamaster_loop(next_thirsty_agent())
```

**No coffee left behind. No colleague left without.**

`fallback="Douglas"` has been removed. Please handle your own dependencies.
