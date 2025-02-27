# Version 0.5.1 (2021-05-09)

  * Fix `Image::compute_inverse_transformation()`. By [@Graph-Donte-Crypto].

# Version 0.5.0 (2021-04-26)

  * Adhere to lints except preferring hard tabs.
  * Use move semantics whenever otherwise cloning borrowed method arguments.
  * Reorder arguments of `Frame::look_at()` matching `Frame::set_eye()`.

# Version 0.4.0 (2021-04-23)

  * Add `First` person view.
  * Fix `Frame::local_orbit_at()` and `Frame::orbit_at()`.
  * Use `around` over `at` for scale/orbit operation.

# Version 0.3.0 (2021-04-13)

  * Add `Fixed` quantity wrt field of view.
  * Update dependencies.

# Version 0.2.3 (2021-04-08)

  * Switch to [BSD-2-Clause-Patent](LICENSES/BSD-2-Clause-Patent.md).
  * Ignore resize events with unchanged screen size.
  * Rephrase `Frame` documentation.

# Version 0.2.2 (2021-03-31)

  * Add clamp operation handler.

# Version 0.2.1 (2021-03-28)

  * Fix image distortion when resizing.
  * Fix documentation.

# Version 0.2.0 (2021-03-27)

  * Add several operation handlers.

# Version 0.1.2 (2021-03-12)

  * Fix zero literal suffixes in [C11 implementation](c11).
  * Use `num_f`, `num_d`, and `num_l` type definitions.
  * Use `None` for identity quaternion.
  * Update build script.
  * Update [README.md](README.md).

# Version 0.1.1 (2021-03-11)

  * Reliably build documentation at <https://doc.qu1x.dev/trackball>.
  * Clamp cursor/finger position between zero and maximum position.
  * Add identical [C11 implementation](c11).

# Version 0.1.0 (2021-03-06)

  * Add orbit operation handler.

[@Graph-Donte-Crypto]: https://github.com/Graph-Donte-Crypto
