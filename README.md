# ☕ The Recursive Moccamaster Loop

### Office protocol for autonomous coffee agents

1. Take a coffee.
2. If you took the last cup, start a new pot.
3. If you don’t want to start a new pot, you cannot take the last cup.
4. Repeat until the office achieves general coffee intelligence.

```python
def coffee_loop(agent):
    if agent is None:
        return "Office closed. Entering sleep mode."

    if pot.has_coffee():
        if pot.remaining_cups == 1:
            if agent.willing_to_brew():
                agent.take_cup()
                agent.brew_new_pot()
            else:
                print("Access denied. Last cup requires write access.")
        else:
            agent.take_cup()

    return coffee_loop(next_thirsty_agent())
```

*Illustrative pseudocode. Please execute the brewing step in real life.*

**You empty it. You prompt the next batch.**  
“Douglas will do it” is a deprecated fallback.
