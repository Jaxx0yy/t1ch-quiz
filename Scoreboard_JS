const PLAYERS = [
  {
    name: "Player 1",
    score: 0,
    id: 1
  },
  {
    name: "Player 2",
    score: 0,
    id: 2
  }
]

let nextId = 3


class AddPlayerForm extends React.Component {
  constructor(props) {
    super(props)
    this.state = { name: '' }
    this._onNameChange = this._onNameChange.bind(this)
    this._onSubmit = this._onSubmit.bind(this)
  }
  
  _onNameChange(e) { 
    this.setState({name: e.target.value})
  }
  
  _onSubmit(e) {
    e.preventDefault()
    this.props.onAdd(this.state.name)
    this.setState({name: ''})
  }
  
  render () {
    return (
      <div className="add-player-form">
        <form onSubmit={this._onSubmit}>
          <input type="text" value={this.state.name} onChange={this._onNameChange} />
          <input type="submit" value="Neuen Affe hinzufügen" />
        </form>
      </div>
    )
  }
}
AddPlayerForm.propTypes = {
  onAdd: React.PropTypes.func.isRequired
}


const Stats = (props) => {
  const totalPlayers = props.players.length
  
  return (
    <table className="stats">
      <tbody>
        <tr>
          <td>Stats:</td>
          <td>{totalPlayers}</td>
        </tr>
      </tbody>
    </table>
  )
}

Stats.propTypes = {
  players: React.PropTypes.array.isRequired
};

const Header = (props) => (
  <div className="header">
    <Stats players={props.players}/>
    <h1>{props.title}</h1>
  </div>
)

Header.propTypes = {
  title: React.PropTypes.string.isRequired,
  players: React.PropTypes.array.isRequired
};

const Counter = (props) => (
  <div className="counter">
    <button className="counter-action decrement" onClick={function() {props.onChange(-1);}} > - </button>
    <div className="counter-score"> {props.score} </div>
    <button className="counter-action increment" onClick={function() {props.onChange(1);}}> + </button>
  </div>
)

Counter.propTypes = {
  score: React.PropTypes.number.isRequired,
  onChange: React.PropTypes.func.isRequired
}

const Player = (props) => (
  <div className="player">
    <div className="player-name">
      <a className="remove-player" onClick={props.onRemove}>✖</a>
      {props.name}
    </div>
    <div className="player-score">
      <Counter score={props.score} onChange={props.onScoreChange} />
    </div>
  </div>
)

Player.propTypes = {
  name: React.PropTypes.string.isRequired,
  score: React.PropTypes.number.isRequired,
  onScoreChange: React.PropTypes.func.isRequired,
  onRemove: React.PropTypes.func.isRequired
};

class Application extends React.Component {
  constructor(props) {
    super(props)
    // Set the initial state
    this.state = { players: this.props.initialPlayers }
    // Bind custom methods
    this._onScoreChange = this._onScoreChange.bind(this)
    this._onPlayerAdd = this._onPlayerAdd.bind(this)
    this._onRemovePlayer = this._onRemovePlayer.bind(this)
  }
  
  _onScoreChange (index, delta) {
    this.state.players[index].score += delta
    this.setState(this.state)
  }
    
  _onPlayerAdd (name) {
    this.state.players.push({
      name: name,
      score: 0,
      id: nextId
    });
    this.setState(this.state)
    nextId += 1
  }
    
  _onRemovePlayer (index) {
    this.state.players.splice(index, 1)
    this.setState(this.state)
  }
  
  render () {
    return (
      <div className="scoreboard">
        <Header title={this.props.title} players={this.state.players} />
      
        <div className="players">
          {this.state.players.map((player, index) =>
            <Player 
              onScoreChange={(delta) => this._onScoreChange(index, delta)}
              onRemove={() => this._onRemovePlayer(index)}
              name={player.name} 
              score={player.score} 
              key={player.id} />
          )}
        </div>
        <AddPlayerForm onAdd={this._onPlayerAdd} />
      </div>
    );
  }
}

Application.propTypes = {
  title: React.PropTypes.string,
  initialPlayers: React.PropTypes.arrayOf(React.PropTypes.shape({
    name: React.PropTypes.string.isRequired,
    score: React.PropTypes.number.isRequired,
    id: React.PropTypes.number.isRequired
  })).isRequired
}

Application.defaultProps = {
  title: "Brain Battle"
}

// Load the app into the DOM
ReactDOM.render(
  <Application initialPlayers={PLAYERS} />,
  document.getElementById('App')
)