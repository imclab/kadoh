var LIB_DIR     = __dirname + '/lib/';
var DIST_DIR    = __dirname + '/dist/';
var JsDoc3_CONF = __dirname + '/doc/JsDocConf.json';
var JsDoc3_EXEC = __dirname + '/doc/jsdoc3/jsdoc';

var UI_FILES = {
  mainline : {
    conf  : __dirname + '/apps/mainline/conf.json',
    index : __dirname + '/apps/mainline/index.html',
    app   : __dirname + '/apps/mainline/app.js'
  },
  udp : {
    conf  : __dirname + '/apps/udp/conf.json',
    index : __dirname + '/apps/udp/index.html',
    app   : __dirname + '/apps/udp/app.js'
  },
  xmpp : {
    conf  : __dirname + '/apps/xmpp/conf.json',
    index : __dirname + '/apps/xmpp/index.html',
    app   : __dirname + '/apps/xmpp/app.js'
  },
  boilerplate : {
    app   : __dirname + '/apps/boilerplate/app.js'
  }
};

var FS     = require('fs');
var PATH   = require('path');
var PROC   = require('child_process');
var COLORS = require('colors');
var UI     = require(__dirname + '/UI/generator');

// ------------ TESTS ------------
namespace('test', function() {

  desc('Testing in the browser');
  task('browser', function() {
    jake.Task['build:test'].execute();

    var jasmine = require('jasmine-runner');
    jasmine.run({
      command : 'mon' ,
      cwd     : __dirname ,
      args    : []
    });
  });
});


// ------------ RUN SERVER ------------

namespace('run', function() {
  
  function run(type) {
    return function(port) {
      port = parseInt(port, 10) || 8080 ;
      require(UI_FILES[type].app).server.listen(port);
      console.log('Server running on http://localhost:'+port);
    }
  }

  desc('Run the mainline proxy app server');
  task('mainline', ['generate:mainline'], run('mainline'));

  desc('Run the udp proxy app server');
  task('udp', ['generate:udp'], run('udp'));

  desc('Run the xmpp app server');
  task('xmpp', ['generate:xmpp'], run('xmpp'));

  desc('Run the boilerplate app server');
  task('boilerplate', run('boilerplate'));
});