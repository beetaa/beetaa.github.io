{"filter":false,"title":"2014-11-12-saving-data-with-ionic-using-html5.md","tooltip":"/_posts/blog/2014-11-12-saving-data-with-ionic-using-html5.md","undoManager":{"mark":100,"position":100,"stack":[[{"group":"doc","deltas":[{"action":"removeText","range":{"start":{"row":20,"column":13},"end":{"row":20,"column":14}},"text":" "}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":13},"end":{"row":20,"column":14}},"text":"l"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":14},"end":{"row":20,"column":15}},"text":"o"}]}],[{"group":"doc","deltas":[{"action":"removeText","range":{"start":{"row":20,"column":14},"end":{"row":20,"column":15}},"text":"o"}]}],[{"group":"doc","deltas":[{"action":"removeText","range":{"start":{"row":20,"column":13},"end":{"row":20,"column":14}},"text":"l"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":5},"end":{"row":20,"column":6}},"text":" "}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":11},"end":{"row":20,"column":12}},"text":" "}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":15},"end":{"row":20,"column":16}},"text":" "}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":16},"end":{"row":20,"column":17}},"text":"l"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":17},"end":{"row":20,"column":18}},"text":"o"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":18},"end":{"row":20,"column":19}},"text":"c"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":19},"end":{"row":20,"column":20}},"text":"a"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":20},"end":{"row":20,"column":21}},"text":"l"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":21},"end":{"row":20,"column":22}},"text":" "}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":22},"end":{"row":20,"column":23}},"text":"s"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":23},"end":{"row":20,"column":24}},"text":"t"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":24},"end":{"row":20,"column":25}},"text":"r"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":25},"end":{"row":20,"column":26}},"text":"o"}]}],[{"group":"doc","deltas":[{"action":"removeText","range":{"start":{"row":20,"column":25},"end":{"row":20,"column":26}},"text":"o"}]}],[{"group":"doc","deltas":[{"action":"removeText","range":{"start":{"row":20,"column":24},"end":{"row":20,"column":25}},"text":"r"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":24},"end":{"row":20,"column":25}},"text":"o"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":25},"end":{"row":20,"column":26}},"text":"r"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":26},"end":{"row":20,"column":27}},"text":"a"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":27},"end":{"row":20,"column":28}},"text":"g"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":28},"end":{"row":20,"column":29}},"text":"e"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":29},"end":{"row":20,"column":30}},"text":" "}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":30},"end":{"row":20,"column":31}},"text":"a"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":31},"end":{"row":20,"column":32}},"text":"p"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":32},"end":{"row":20,"column":33}},"text":"i"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":20,"column":33},"end":{"row":21,"column":0}},"text":"\n"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":21,"column":0},"end":{"row":22,"column":0}},"text":"\n"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":22,"column":0},"end":{"row":22,"column":4}},"text":"    "}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":22,"column":4},"end":{"row":22,"column":48}},"text":"myApp.controller('Login', function($scope) {"},{"action":"insertText","range":{"start":{"row":22,"column":48},"end":{"row":23,"column":0}},"text":"\n"},{"action":"insertLines","range":{"start":{"row":23,"column":0},"end":{"row":40,"column":0}},"lines":["    $scope.login = function(username, password) {","        window.localStorage.setItem(\"username\", username);","        window.localStorage.setItem(\"password\", password);","    };"," ","    $scope.isLoggedIn = function() {","        if(window.localStorage.getItem(\"username\") !== undefined && window.localStorage.getItem(\"password\") !== undefined) {","            return true;","        } else {","            return false;","        }","    };"," ","    $scope.logout = function() {","        window.localStorage.removeItem(\"username\");","        window.localStorage.removeItem(\"password\");","    };"]},{"action":"insertText","range":{"start":{"row":40,"column":0},"end":{"row":40,"column":3}},"text":"});"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":23,"column":0},"end":{"row":23,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":24,"column":0},"end":{"row":24,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":25,"column":0},"end":{"row":25,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":26,"column":0},"end":{"row":26,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":27,"column":0},"end":{"row":27,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":28,"column":0},"end":{"row":28,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":29,"column":0},"end":{"row":29,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":30,"column":0},"end":{"row":30,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":31,"column":0},"end":{"row":31,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":32,"column":0},"end":{"row":32,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":33,"column":0},"end":{"row":33,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":34,"column":0},"end":{"row":34,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":35,"column":0},"end":{"row":35,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":36,"column":0},"end":{"row":36,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":37,"column":0},"end":{"row":37,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":38,"column":0},"end":{"row":38,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":39,"column":0},"end":{"row":39,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":40,"column":0},"end":{"row":40,"column":4}},"text":"    "}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":41,"column":0},"end":{"row":42,"column":0}},"text":"\n"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":0},"end":{"row":42,"column":1}},"text":"$"}]}],[{"group":"doc","deltas":[{"action":"removeText","range":{"start":{"row":42,"column":0},"end":{"row":42,"column":1}},"text":"$"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":0},"end":{"row":42,"column":1}},"text":"#"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":1},"end":{"row":42,"column":2}},"text":"#"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":2},"end":{"row":42,"column":3}},"text":"#"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":3},"end":{"row":42,"column":4}},"text":" "}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":4},"end":{"row":42,"column":5}},"text":"s"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":5},"end":{"row":42,"column":6}},"text":"h"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":6},"end":{"row":42,"column":7}},"text":"i"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":7},"end":{"row":42,"column":8}},"text":"y"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":8},"end":{"row":42,"column":9}},"text":"o"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":9},"end":{"row":42,"column":10}},"text":"n"}]}],[{"group":"doc","deltas":[{"action":"removeText","range":{"start":{"row":42,"column":9},"end":{"row":42,"column":10}},"text":"n"}]}],[{"group":"doc","deltas":[{"action":"removeText","range":{"start":{"row":42,"column":8},"end":{"row":42,"column":9}},"text":"o"}]}],[{"group":"doc","deltas":[{"action":"removeText","range":{"start":{"row":42,"column":7},"end":{"row":42,"column":8}},"text":"y"}]}],[{"group":"doc","deltas":[{"action":"removeText","range":{"start":{"row":42,"column":6},"end":{"row":42,"column":7}},"text":"i"}]}],[{"group":"doc","deltas":[{"action":"removeText","range":{"start":{"row":42,"column":5},"end":{"row":42,"column":6}},"text":"h"}]}],[{"group":"doc","deltas":[{"action":"removeText","range":{"start":{"row":42,"column":4},"end":{"row":42,"column":5}},"text":"s"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":4},"end":{"row":42,"column":6}},"text":"使用"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":6},"end":{"row":42,"column":7}},"text":" "}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":7},"end":{"row":42,"column":8}},"text":"J"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":8},"end":{"row":42,"column":9}},"text":"s"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":9},"end":{"row":42,"column":10}},"text":"o"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":10},"end":{"row":42,"column":11}},"text":"n"}]}],[{"group":"doc","deltas":[{"action":"removeText","range":{"start":{"row":42,"column":10},"end":{"row":42,"column":11}},"text":"n"}]}],[{"group":"doc","deltas":[{"action":"removeText","range":{"start":{"row":42,"column":9},"end":{"row":42,"column":10}},"text":"o"}]}],[{"group":"doc","deltas":[{"action":"removeText","range":{"start":{"row":42,"column":8},"end":{"row":42,"column":9}},"text":"s"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":8},"end":{"row":42,"column":9}},"text":"S"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":9},"end":{"row":42,"column":10}},"text":"O"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":10},"end":{"row":42,"column":11}},"text":"N"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":11},"end":{"row":42,"column":12}},"text":"."}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":12},"end":{"row":42,"column":13}},"text":"s"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":13},"end":{"row":42,"column":14}},"text":"t"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":14},"end":{"row":42,"column":15}},"text":"r"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":15},"end":{"row":42,"column":16}},"text":"i"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":16},"end":{"row":42,"column":17}},"text":"g"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":17},"end":{"row":42,"column":18}},"text":"i"}]}],[{"group":"doc","deltas":[{"action":"removeText","range":{"start":{"row":42,"column":17},"end":{"row":42,"column":18}},"text":"i"}]}],[{"group":"doc","deltas":[{"action":"removeText","range":{"start":{"row":42,"column":16},"end":{"row":42,"column":17}},"text":"g"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":16},"end":{"row":42,"column":17}},"text":"n"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":17},"end":{"row":42,"column":18}},"text":"g"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":18},"end":{"row":42,"column":19}},"text":"i"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":19},"end":{"row":42,"column":20}},"text":"f"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":20},"end":{"row":42,"column":21}},"text":"y"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":21},"end":{"row":42,"column":22}},"text":" "}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":22},"end":{"row":42,"column":23}},"text":"和"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":23},"end":{"row":42,"column":24}},"text":" "}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":24},"end":{"row":42,"column":28}},"text":"JSON"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":28},"end":{"row":42,"column":29}},"text":"."}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":29},"end":{"row":42,"column":30}},"text":"p"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":30},"end":{"row":42,"column":31}},"text":"a"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":31},"end":{"row":42,"column":32}},"text":"r"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":32},"end":{"row":42,"column":33}},"text":"s"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":33},"end":{"row":42,"column":34}},"text":"e"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":34},"end":{"row":42,"column":35}},"text":" "}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":35},"end":{"row":42,"column":36}},"text":"来"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":36},"end":{"row":42,"column":38}},"text":"处理"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":38},"end":{"row":42,"column":40}},"text":"复杂"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":40},"end":{"row":42,"column":42}},"text":"数据"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":42,"column":42},"end":{"row":43,"column":0}},"text":"\n"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":43,"column":0},"end":{"row":44,"column":0}},"text":"\n"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":44,"column":0},"end":{"row":44,"column":4}},"text":"    "}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":44,"column":4},"end":{"row":44,"column":57}},"text":"myApp.controller('Profile', function($scope, $http) {"},{"action":"insertText","range":{"start":{"row":44,"column":57},"end":{"row":45,"column":0}},"text":"\n"},{"action":"insertLines","range":{"start":{"row":45,"column":0},"end":{"row":55,"column":0}},"lines":["    $http.get(\"https://api.example.com/profile\", { params: { \"api_key\": \"some_key_here\" } })","        .success(function(data) {","            $scope.profile = data;","            window.localStorage.setItem(\"profile\", JSON.stringify(data));","        })","        .error(function(data) {","            if(window.localStorage.getItem(\"profile\") !== undefined) {","                $scope.profile = JSON.parse(window.localStorage.getItem(\"profile\"));","            }","        });"]},{"action":"insertText","range":{"start":{"row":55,"column":0},"end":{"row":55,"column":3}},"text":"});"}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":45,"column":0},"end":{"row":45,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":46,"column":0},"end":{"row":46,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":47,"column":0},"end":{"row":47,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":48,"column":0},"end":{"row":48,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":49,"column":0},"end":{"row":49,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":50,"column":0},"end":{"row":50,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":51,"column":0},"end":{"row":51,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":52,"column":0},"end":{"row":52,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":53,"column":0},"end":{"row":53,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":54,"column":0},"end":{"row":54,"column":4}},"text":"    "},{"action":"insertText","range":{"start":{"row":55,"column":0},"end":{"row":55,"column":4}},"text":"    "}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":55,"column":7},"end":{"row":56,"column":0}},"text":"\n"},{"action":"insertText","range":{"start":{"row":56,"column":0},"end":{"row":56,"column":4}},"text":"    "}]}],[{"group":"doc","deltas":[{"action":"insertText","range":{"start":{"row":56,"column":4},"end":{"row":57,"column":0}},"text":"\n"},{"action":"insertText","range":{"start":{"row":57,"column":0},"end":{"row":57,"column":4}},"text":"    "}]}]]},"ace":{"folds":[],"scrolltop":0,"scrollleft":0,"selection":{"start":{"row":9,"column":10},"end":{"row":9,"column":10},"isBackwards":false},"options":{"guessTabSize":true,"useWrapMode":false,"wrapToView":true},"firstLineState":0},"timestamp":1415802100247,"hash":"0aaabfee896ac2f1dc5929b1fc9c736ef147c4ae"}