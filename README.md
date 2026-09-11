# fix(coffee): keep the next batch ready

**Status:** Awaiting human review  
**Reviewer:** Whoever takes the next cup  
**Priority:** Increases as the pot empties

## Problem

Coffee consumption scales with the team. Coffee production scales with Douglas.

## Proposed change

**One cup. One contribution.** Before taking coffee, complete the first applicable action:

1. **Tank empty?** Fill it for the next batch.
2. **Filter or grounds used?** Replace both.
3. **Ready to brew, with room for the entire next batch?** Start brewing.

Then pass the task to the next coffee drinker. Preparing water, a fresh filter and coffee does not require an empty pot. If brewing is running, or everything is ready but the pot is too full, no action is needed this time.

> **The last cup is yours only when the next brew is running.**  
> Completing a preparation step does not override this requirement.

## Implementation

```python
# Pseudocode. Human execution required.

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

    contribute()  # One action per cup.

    last_cup_locked = pot.cups <= 1 and not machine.is_brewing()
    if pot.cups > 0 and not last_cup_locked:
        agent.pour_coffee()

    return moccamaster_loop(next_thirsty_agent())
```

## Review checklist

- [ ] I can identify an empty water tank.
- [ ] I understand that fresh coffee requires fresh grounds.
- [ ] I can press a button without delegating to an AI agent.
- [ ] I accept that “I was going to” is not a brewing state.

## Breaking change

`fallback="Douglas"` has been removed.

**Approval requested. Implementation expected at your next cup.**
