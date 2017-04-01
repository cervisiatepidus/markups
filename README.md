Beispiel für die Nutzung von Webcomponents
==========================================

Hier soll gezeigt werden wie man Webcomponents einsetzen kann. Dabei stützen wir uns auf das Beispiel von Marcus Fihlon. Siehe https://github.com/McPringle/sessions/tree/master/WebComponents%20Introduction

Schritte:
---------

develop branch auschecken

        npm init
        npm i @polymer/iron-ajax
        npm i @polymer/paper-card
        npm i @polymer/paper-progress


#### schritt1 ####

hier sind bereits die externen Web Components per NPM installiert


#### schritt2 ####

* Datei index.html

        <title>WEBS Server Dashboard</title>
        <script src="node_modules/webcomponents.js/webcomponents.min.js"></script>

* Ordner app_components/dashboard-app

* Datei app_components/dashboard-app/dashboard-app.html
    * vorgenerierten Inhalt löschen
    
    
 
          <link rel="import" href="../../node_modules/@polymer/polymer/polymer.html"/>
                <dom-module id="dashboard-app">
                        <template>
                                <h1>WEBS Server Dashboard</h1>
                        </template>

                    <script>
                        Polymer({
                            is: 'dashboard-app'
                        });
                    </script>

                </dom-module>


* index.html

        <link rel="import" href="app_components/dashboard-app/dashboard-app.html"/>

        <body>

            <dashboard-app></dashboard-app>

        </body>


* app_components/dashboard-app/dashboard-app.html

        <link rel="import" href="../../node_modules/@polymer/paper-material/paper-material.html"/>
        <link rel="import" href="../../node_modules/@polymer/paper-styles/paper-styles.html"/>

        <dom-module id="dashboard-app">
            <template>
                <style>
                    :host {
                        display: block;
                    }
                    * {
                        font-family: 'Roboto', sans-serif;
                    }
                    paper-material {
                        margin: 2em;
                        padding: 0.5em 1em 0.5em 1em;
                    }
                </style>

                <paper-material elevation="5">
                    <h1>WEBS Server Dashboard</h1>
                </paper-material>
            </template>



        </dom-module>

* Ergebnis zeigen

#### schritt3 ####

* Ordner app_components/dashboard-server-list
* Datei app_components/dashboard-server-list/dashboard-server-list
    * vorgenerierten Inhalt löschen


                <link rel="import" href="../../node_modules/@polymer/polymer/polymer.html"/>
                <link rel="import" href="../../node_modules/@polymer/iron-ajax/iron-ajax.html"/>

                <dom-module id="dashboard-server-list">
                    <template>
                        Inhalt
                    </template>

                    <script>
                        Polymer({
                            is: 'dashboard-server-list'
                        });
                    </script>

                </dom-module>

* app_components/dashboard-app/dashboard-app.html

        <link rel="import" href="../../app_components/dashboard-server-list/dashboard-server-list.html"/>


        <dashboard-server-list></dashboard-server-list>


* Ergebnis zeigen (Inhalt)

* app_components/dashboard-server-list/dashboard-server-list
    * Inhalt löschen, stattdessen

            <template>
                <iron-ajax auto url="../../api/metrics.json" handle-as="json"
                            last-response="{{ajaxResponse}}"></iron-ajax>
                {{ajaxResponse}}
            </template>

* Ergebnis zeigen ([object Object],[object Object])

* app_components/dashboard-server-list/dashboard-server-list

                <template is="dom-repeat" items="[[ajaxResponse]]">
                                {{item}}
                </template>

* Ergebnis zeigen ([object Object],[object Object])

* Ordner app_components/dashboard-info-panel
* Datei app_components/dashboard-info-panel/dashboard-info-panel

        <link rel="import" href="../../node_modules/@polymer/polymer/polymer.html"/>
        <link rel="import" href="../../node_modules/@polymer/paper-card/paper-card.html"/>
        <link rel="import" href="../../node_modules/@polymer/paper-progress/paper-progress.html"/>


        <dom-module id="dashboard-info-panel">
            <template>
                Items
            </template>
            <script>
                Polymer({
                    is: 'dashboard-info-panel'
                });
            </script>

        </dom-module>

* app_components/dashboard-server-list/dashboard-server-list

        <link rel="import" href="../../app_components/dashboard-info-panel/dashboard-info-panel.html"/>


                <template is="dom-repeat" items="[[ajaxResponse]]">
                    <dashboard-info-panel></dashboard-info-panel>
                </template>

* Ergebnis zeigen (Items, Items)


* app_components/dashboard-server-list/dashboard-server-list

        <template is="dom-repeat" items="[[ajaxResponse]]">
            <dashboard-info-panel serverdata="{{item}}"></dashboard-info-panel>
        </template>

* app_components/ashboard-info-panel/dashboard-info-panel

            <template>
                {{serverdata.name}}
            </template>
            <script>
                Polymer({
                    is: 'dashboard-info-panel',
                    properties: {
                        serverdata: {
                            type: Object,
                            value: null
                        }
                    }
                });
            </script>

* Ergebnis zeigen (Merkur Venus Erde)

* app_components/dashboard-info-panel/dashboard-info-panel

                <style>
                    paper-card {
                        margin: 10px;
                        padding: 5px;
                        width: 300px;
                        --paper-card-header-image-text : {
                            color: #ffffff;
                            font-size: 30px;
                            text-align: center;
                            left: 0;
                            right: 0;
                        }
                    }
                    label {
                        display: inline-block;
                        width: 80px;
                    }
                    paper-progress {
                        display: inline-block;
                        width: 200px;
                    }
                </style>

                <paper-card heading="{{serverdata.name}}" image="images/{{serverdata.name}}.jpg">


* Ergebnis zeigen (Bilder!!!)

* app_components/dashboard-info-panel/dashboard-info-panel

                <paper-card heading="{{serverdata.name}}" image="images/{{serverdata.name}}.jpg">
                    <label>IP:</label>{{serverdata.ip}}<br />
                    <label>CPU:</label><paper-progress value="{{serverdata.cpu}}"></paper-progress>
                    <label>MEMORY:</label><paper-progress value="{{serverdata.memory}}"></paper-progress>
                    <label>DISK:</label><paper-progress value="{{serverdata.disk}}"></paper-progress>

                </paper-card>

* Ergebnis zeigen (fertig)
    * JSON bearbeiten + STRG F5
