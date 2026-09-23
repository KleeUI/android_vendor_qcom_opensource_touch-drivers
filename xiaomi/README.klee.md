# Xiaomi ST SPI input modules

These sources are imported from LineageOS/android_kernel_xiaomi_sm8450,
revision 65d81f0b6bf8eac90ab562932a6dd7a10df06ebe. The input sources are
unchanged from its parent e682ed2de56fd2841ef35741c4d0f03599ffd561, the
revision identified by the working prebuilt Cupid kernel's boot log.
Original copyright and GPL notices are retained in every imported file.

The external Kbuild emits hwid.ko, xiaomi_touch.ko and fts_touch_spi.ko.
Cupid's existing st,spi node and st_fts_l3.ftb firmware names are retained.
Load hwid with project=2 for Cupid; the parameter uses the upstream L3 ID.

The ST driver owns the Qualcomm panel notifier subscription and forwards
notifications to the Xiaomi touch interface after handling its own event.
This preserves the controller/interface order without adding private client
IDs to the kernel's public panel notifier API. Gesture deferral and pending
event clearing remain in the Xiaomi interface. Its initialization failures
return the allocation/device error and unwind the resources already created.

Validation before integration: Clang 21 build, matching
5.10.252-gki-klee vermagic, and a combined 397-module dependency, symbol
ownership and CRC check. Hardware operation still requires device testing.
