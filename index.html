const config = {
  type: Phaser.AUTO,
  width: window.innerWidth,
  height: window.innerHeight,
  parent: null,
  physics: { default: 'arcade', arcade: { debug: false } },
  scale: { mode: Phaser.Scale.RESIZE, autoCenter: Phaser.Scale.CENTER_BOTH },
  scene: { preload, create, update },
  plugins: {
    global: [{
      key: 'rexVirtualJoystick',
      plugin: rexvirtualjoystickplugin,
      start: true
    }]
  }
};
const game = new Phaser.Game(config);

function preload() {
  this.load.image('player','https://i.imgur.com/4AiXzf8.png');
  this.load.image('bullet','https://i.imgur.com/WP2Qe0K.png');
  this.load.image('enemy','https://i.imgur.com/0rVeh4D.png');
  this.load.image('joystick_base','https://i.imgur.com/8wKQZQk.png');
  this.load.image('joystick_thumb','https://i.imgur.com/0KX2YkB.png');
  this.load.image('btn_fire','https://i.imgur.com/6XQw4.png');
}

let player, joystick, fireButton, bullets, lastShot = 0, enemies;

function create() {
  player = this.physics.add.sprite(400,300,'player').setScale(0.5).setCollideWorldBounds(true);

  // joystick no canto inferior-esquerdo
  joystick = this.plugins.get('rexVirtualJoystick').add(this, {
    x: 100, y: this.scale.height - 100,
    radius: 60,
    base: this.add.image(0,0,'joystick_base').setAlpha(0.6),
    thumb: this.add.image(0,0,'joystick_thumb').setAlpha(0.8),
    dir: '8dir',
    forceMin: 8
  });
  joystick.setScrollFactor(0);

  // botão de atirar no canto inferior-direito
  fireButton = this.add.image(this.scale.width - 90, this.scale.height - 90, 'btn_fire').setInteractive().setAlpha(0.9);
  fireButton.setScrollFactor(0);
  fireButton.on('pointerdown', (p)=> doFire.call(this, p));
  // suportar resize: reposicionar UI quando canvas muda
  this.scale.on('resize', (gameSize) => {
    const { width, height } = gameSize;
    joystick.x = 100; joystick.y = height - 100;
    fireButton.x = width - 90; fireButton.y = height - 90;
  });

  // bullets & enemies
  bullets = this.physics.add.group({ classType: Phaser.GameObjects.Image });
  enemies = this.physics.add.group();
  for (let i=0;i<5;i++){
    let e = enemies.create(100 + i*120,100,'enemy').setScale(0.6).setCollideWorldBounds(true);
    e.hp = 3;
  }

  this.physics.add.overlap(bullets, enemies, (b,e) => {
    b.destroy();
    e.hp--;
    if (e.hp<=0) e.destroy();
  });

  // teclado e mouse
  this.keys = this.input.keyboard.addKeys('W,A,S,D,SPACE,LEFT,RIGHT,UP,DOWN');
  this.input.on('pointerdown', (p) => {
    if (p.x < this.scale.width/2) return; // evita atirar ao tocar joystick area
    doFire.call(this, p);
  });
}

function update(time) {
  // movimento via joystick ou teclado
  const speed = 220;
  let vx = 0, vy = 0;
  if (joystick.force > 0) {
    const vec = joystick.force; // magnitude
    const angle = joystick.angle;
    this.physics.velocityFromAngle(angle, joystick.force * 3, player.body.velocity);
  } else {
    let left = this.keys.A.isDown || this.keys.LEFT.isDown;
    let right = this.keys.D.isDown || this.keys.RIGHT.isDown;
    let up = this.keys.W.isDown || this.keys.UP.isDown;
    let down = this.keys.S.isDown || this.keys.DOWN.isDown;
    if (left) vx = -speed;
    if (right) vx = speed;
    if (up) vy = -speed;
    if (down) vy = speed;
    player.setVelocity(vx, vy);
  }

  // inimigos simples seguem
  enemies.getChildren().forEach(e => {
    this.physics.moveToObject(e, player, 80);
  });
}

function doFire(pointer) {
  const now = Date.now();
  if (now - lastShot < 200) return; // fire rate
  lastShot = now;
  // mirar para o pointer (ou frente do jogador se botão)
  let targetX = pointer.worldX !== undefined ? pointer.worldX : pointer.x;
  let targetY = pointer.worldY !== undefined ? pointer.worldY : pointer.y;
  // se o input veio do botão, atira na direção para a frente (mouse pos fallback)
  const angle = Phaser.Math.Angle.Between(player.x, player.y, targetX, targetY);
  const b = bullets.create(player.x, player.y, 'bullet').setScale(0.3);
  this.physics.velocityFromRotation(angle, 500, b.body.velocity);
  setTimeout(()=>{ if (b && b.destroy) b.destroy(); }, 1500);
}
