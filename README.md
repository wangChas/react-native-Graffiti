#react-native-Graffiti
draw on an existing image
## Getting Started

### iOS
1. `npm install`;
2. `react-native link`;
3. run in Xcode.


## Usage
```javascript
    import React, {Component} from 'react';
    import {
        View,
        Text,
        TouchableHighlight,
        TouchableOpacity,
        StyleSheet,
        StatusBar,
        Slider
    } from 'react-native';
    import SketchView from 'react-native-sketch-view';


    const sketchViewConstants = SketchView.constants;

    const tools = {};

    let localPath = ''; //set local picture url which you want

    tools[sketchViewConstants.toolType.pen.id] = {
        id: sketchViewConstants.toolType.pen.id,
        name: sketchViewConstants.toolType.pen.name,
        nextId: sketchViewConstants.toolType.eraser.id
    };
    tools[sketchViewConstants.toolType.eraser.id] = {
        id: sketchViewConstants.toolType.eraser.id,
        name: sketchViewConstants.toolType.eraser.name,
        nextId: sketchViewConstants.toolType.pen.id
    };


    export default class Doodle extends Component {

        constructor(props) {
            super(props);
            this.state = {
                toolSelected: sketchViewConstants.toolType.pen.id,
                penThickness: 3,
                color: '#FFFFFF',

            };
        }

        onSketchSave(saveEvent) {
            this.props.onSave && this.props.onSave(saveEvent);
        }

        renderColorButton = (color) => {
            const active = color === this.state.color;

            return (
                <TouchableOpacity
                    onPress={() => this.setState({color: color})}
                    style={[
                        styles.colorButton,
                        {
                            backgroundColor: active ? '#000' : color,
                            borderColor: color,
                        },
                    ]}/>
            );
        };
        render() {
            return (
                <View style={{flex:1, flexDirection: 'column'}}>
                    <StatusBar barStyle={this.state.path ? 'default' : 'dark-content'} />
                    <View style={styles.colorsBar}>
                        {this.renderColorButton('#20BBFC')}
                        {this.renderColorButton('#2DFD2F')}
                        {this.renderColorButton('#FD28F9')}
                        {this.renderColorButton('#EA212E')}
                        {this.renderColorButton('#FD7E24')}
                        {this.renderColorButton('#FFFA38')}
                        {this.renderColorButton('#FFFFFF')}
                    </View>
                    <Slider style={{marginLeft: 10, marginRight: 10}}
                            onSlidingComplete={()=>console.log('当前的值为'+this.state.penThickness)}
                            onValueChange={(value)=>this.setState({penThickness: value})}
                            maximumValue={20}
                            minimumValue={1}
                            step={1}
                            value={this.state.penThickness}/>
                    <SketchView
                        ref="sketchRef"
                        style={{flex:1, alignItems:'center',  backgroundColor: '#EEE'}}
                        toolColor={this.state.color}
                        selectedTool={this.state.toolSelected}
                        onSaveSketch={this.onSketchSave.bind(this)}
                        toolThickness={this.state.penThickness}
                        // localSourceImagePath={this.props.localSourceImagePath}/>
                        localSourceImagePath={localPath}/>

                    <View style={{flexDirection: 'row', backgroundColor: '#EEE'}}>
                        <TouchableHighlight underlayColor={"#CCC"} style={{
                            flex: 1,
                            alignItems: 'center',
                            paddingVertical: 20,
                            borderLeftWidth: 1,
                            borderRightWidth: 1,
                            borderColor: '#DDD'
                        }} onPress={() => {
                            this.refs.sketchRef.saveSketch()
                        }}>
                            <Text style={{color: '#888', fontWeight: '600'}}>SAVE
                            </Text>
                        </TouchableHighlight>
                    </View>
                </View>
            );
        }
    }

    const styles = StyleSheet.create({
        colorsBar: {
            flexDirection: 'row',
            justifyContent: 'space-between',
            paddingHorizontal: 20,
            paddingTop: 20,
        },
        colorButton: {
            borderRadius: 50,
            borderWidth: 8,
            width: 25,
            height: 25,
        },
    });
```

## Explain
you can draw on a existing image.
the same apis and props as react-native-sketch-view.But there are some bug of Eraser and clear.
check out the save path from Xcode output window.


## Source
This code was copied from https://github.com/jgrancher/react-native-sketch and https://github.com/keshavkaul/react-native-sketch-view.
I just took the example for draw on an existing image.