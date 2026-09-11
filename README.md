# ☕ The Recursive Moccamaster Loop

### Office protocol for autonomous coffee agents

Our mission: continuous coffee availability. Human intervention is a feature.

1. **Is there water in the tank?** No → add water for the next batch. **Even if the pot is full of coffee.**
2. **Are there fresh grounds and a fresh filter?** No → replace the used filter and grounds with a fresh filter and fresh coffee. **Even if the pot is full of coffee.**
3. **Is there enough room in the pot for the entire next batch?** Yes → **start brewing.** Otherwise, keep the next batch ready and check again as coffee is taken.

Do the preparation checks between brewing cycles. If a cycle is already running, let it finish before refilling the tank or changing the filter.

> **Under no circumstances may you take the last cup without having activated a new brewing cycle.**
>
> No new cycle running? Last cup locked. “I was going to” is not a brewing state.

```python
# Illustrative pseudocode: the human is the runtime.

def prepare_and_brew():
    if machine.is_brewing():
        return  # Let the current cycle finish.

    if not tank.has_water():
        tank.fill_for_next_batch()  # Even if the coffee pot is full.

    if not basket.has_fresh_filter_and_coffee():
        basket.replace_with_fresh_filter_and_coffee()

    if pot.free_space() >= tank.next_batch_volume():
        machine.start_brewing()


def coffee_loop(agent):
    if agent is None:
        return "Office closed. Entering sleep mode."

    prepare_and_brew()

    if pot.has_coffee():
        if pot.would_empty_after_one_cup() and not machine.is_brewing():
            print("403 Forbidden: activate a new brew before the last cup.")
        else:
            agent.take_cup()
            prepare_and_brew()  # Your cup may have made room to brew.

    return coffee_loop(next_thirsty_agent())
```

**Keep the coffee flowing. Be the agent that takes action.**  
“Douglas will do it” is a deprecated fallback.
