# How to integrate two tools?

The problem we try solve by having all in one package is to ease the changing of APIs without unknowingly breaking something in another integrative package. It's to reduce subtle bugs when we upgrade production. Your tool should be defined under `cg/apps/yourtool.py` and the integration under `cg/meta/yourintegration` and the invoking command under `cg/cli/yourcommand.py`.
