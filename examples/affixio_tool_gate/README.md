AffixIO Tool Gate

This example shows how to put an allow, deny or review decision in front of an agent tool call using the external AffixIO NeMo plugin. The check runs before the tool executes, and a failed check blocks the call.

How it works

The plugin asks AffixIO whether the tool call should run, then acts on the answer.

NeMo Agent Toolkit -> AffixIO plugin -> AffixIO API -> ALLOW / DENY / REVIEW -> tool runs or is blocked

ALLOW runs the tool.
DENY blocks the tool.
REVIEW blocks unless you add a separate approval step.
An API failure blocks the call because fail_closed is set to true.
Requirements

A NeMo Agent Toolkit environment on Python 3.11 or later.
An AffixIO API key. The free tier includes 100 proofs and does not need a card.
Install

shell
uv pip install -e examples/affixiotoolgate
export AFFIXIOAPIKEY="aio_…"

Run

shell
nat run --configfile examples/affixiotool_gate/configs/config.yml --input "run the protected tool"

What you should see

The agent requests the tool, the plugin sends a decision request to AffixIO, and the tool runs only when the decision is ALLOW. Set the policy in configs/config.yml to exclude the tool and the same run blocks instead.

Make it yours

Replace the protected_tool entry in configs/config.yml with the tool you want to protect, and list that tool name under policy.allowed_tools. Several functions can share the same gate.

Links

Plugin source: https://github.com/AffixIO/affixio-nemo-plugin
AffixIO: https://www.affix-io.com/
NeMo Agent Toolkit: https://github.com/NVIDIA/NeMo-Agent-Toolkit
