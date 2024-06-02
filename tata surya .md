function setup() {
  createCanvas(windowWidth, windowHeight - 4, WEBGL);
  camera(0, -1000, 2200);
  sun = new CelestialObject(300, 0, null, loadImage("Textures/sun.jpg"));
  m = new CelestialObject(7.5, 400, sun, loadImage("Textures/mercury.jpg"));
  // Objek-objek benda langit lainnya diinisialisasi di sini...
  starTexture = loadImage('Textures/2k_stars_milky_way.jpg');
}
class CelestialObject {

  constructor(radius, distance, parent, tex) {
    this.radius = radius;
    this.distance = distance;
    this.orbitLength = distance * 2 * PI;
    this.angle = random(2 * PI);
    this.tex = tex;
    this.children = [];
    this.parent = parent;
    if (parent) {
      parent.children.push(this);
    }
  }
  if (this.orbitLength > 0) {
  let speed = pow((width - this.distance) / (width), 0.5);
  this.angle += (speed / this.orbitLength) * (2 * PI);
}
 show() {
    push();
    {
      push();
      {
        strokeWeight(0.1);
        stroke(255);
        noFill();
        ellipse(0, 0, this.distance * 2);
      }
      pop();

      rotate(-this.angle);
      translate(this.distance, 0);

      texture(this.tex);
      push();
      rotateX(-PI/2);
      sphere(this.radius);
      pop();
      for (let CelestialObject of this.children) {
        CelestialObject.show();
      }
    }
    pop();
  }
