# trackball

Virtual Trackball Orbiting via the Exponential Map

[![Build Status][]](https://travis-ci.org/qu1x/trackball)
[![Downloads][]](https://crates.io/crates/trackball)
[![Rust][]](https://www.rust-lang.org)
[![Version][]](https://crates.io/crates/trackball)
[![Documentation][]](https://doc.qu1x.dev/trackball)
[![License][]](https://opensource.org/licenses/BSD-3-Clause)

[Build Status]: https://travis-ci.org/qu1x/trackball.svg
[Downloads]: https://img.shields.io/crates/d/trackball.svg
[Rust]: https://img.shields.io/badge/rust-stable-brightgreen.svg
[Version]: https://img.shields.io/crates/v/trackball.svg
[Documentation]: https://docs.rs/trackball/badge.svg
[License]: https://img.shields.io/crates/l/trackball.svg

This is an alternative trackball technique using exponential map and parallel transport to
preserve distances and angles for inducing coherent and intuitive trackball rotations. For
instance, displacements on straight radial lines through the screen's center are carried to arcs
of the same length on great circles of the trackball. This is in contrast to state-of-the-art
techniques using orthogonal projection which distorts radial distances further away from the
screen's center. This implementation strictly follows the recipe given in the paper of
Stantchev, G.. “Virtual Trackball Modeling and the Exponential Map.” . [S2CID] [44199608].

[S2CID]: https://en.wikipedia.org/wiki/S2CID_(identifier)
[44199608]: https://api.semanticscholar.org/CorpusID:44199608

## Features

  * Common trackball operations split into several operation handlers.
  * Coherent and intuitive orbiting via the exponential map, see [`Orbit`] operation handler.
  * Identical [C11 implementation](c11) for [`Orbit`] operation handler behind `cc` feature gate.
  * Observer frame with [`Frame::look_at()`], [`Frame::scale_at()`], [`Frame::slide()`],
    [`Frame::orbit_at()`] operations.
  * Object inspection mode scaling clip planes by measuring them from target instead of eye.
  * Scale preserving transitioning between orthographic and perspective projection mode.
  * Timing-free touch gesture recognition for slide, orbit, scale, and focus operations.

[`Frame::look_at()`]: https://doc.qu1x.dev/trackball/trackball/struct.Frame.html#method.look_at
[`Frame::scale_at()`]: https://doc.qu1x.dev/trackball/trackball/struct.Frame.html#method.scale_at
[`Frame::slide()`]: https://doc.qu1x.dev/trackball/trackball/struct.Frame.html#method.slide
[`Frame::orbit_at()`]: https://doc.qu1x.dev/trackball/trackball/struct.Frame.html#method.orbit_at

## Example

A trackball camera mode implementation can be as easy as this by delegating events of your 3D
graphics library of choice to the [`Orbit`] operation handler along with other handlers.

```rust
use nalgebra::{Point2, UnitQuaternion, Vector3};
use std::f32::consts::PI;
use trackball::{Frame, Image, Orbit};

/// Trackball camera mode.
pub struct Trackball {
	// Frame wrt camera eye and target.
	frame: Frame<f32>,
	// Image as projection of `Scene` wrt `Frame`.
	image: Image<f32>,
	// Orbit induced by displacement on screen.
	orbit: Orbit<f32>,
}

impl Trackball {
	// Usually, a cursor position event with left mouse button being pressed.
	fn handle_left_button_displacement(&mut self, pos: &Point2<f32>) {
		// Maximum position as screen's width and height.
		let max = self.image.max;
		// Induced rotation in camera space.
		let rot = self.orbit.compute(&pos, &max).unwrap_or_default();
		// Apply induced rotation to local observer frame.
		self.frame.local_orbit(&rot);
	}
	// Event when left mouse button is released again.
	fn handle_left_button_release(&mut self) {
		// Can also or instead be invoked on `Self::handle_left_button_press()`.
		self.orbit.discard();
	}
}
```

## C11 Implementation

Identical [C11 implementation](c11) for [`Orbit`] operation handler behind `cc` feature gate:

```toml
[dependencies]
trackball = { version = "0.1", features = ["cc"] }
```

[`Orbit`]: https://doc.qu1x.dev/trackball/trackball/struct.Orbit.html

## License

[BSD-3-Clause](LICENSE.md)

## Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion
in the works by you shall be licensed as above, without any additional terms or conditions.
