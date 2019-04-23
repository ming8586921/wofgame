![blizzardgame](128px-Blizzard_Entertainment_Logo.svg.png)
# wofgame
The first game for blockchain, see https://wofgame.github.io
# Rule analysis
* 25% dynamic within 3 generations
* 12% weight distribution
* 15% prize pool
* 40% static + dynamic precipitation + weight dividend precipitation
* 3% platform fee

# Source code analysis
## Floating income calculation

```Solidity
function rand(uint256 _length, address _pAddress) 
        private
        view
        returns(uint256) 
{
	uint256 random = uint256(keccak256(abi.encodePacked(block.difficulty, now, _pAddress, inc_)));
	return random%_length;
}

function inc()
	private
        view
        returns(uint256) 
{
	return rand(100, _pAddress) < 50 ? inc_+=3 : inc+=5;
}

```
* Random number generation
* Random seed acquisition

```Solidity
function calc(address _pAddress, uint256 _canIncome, uint256 _day, uint256 _probFixResW)
        private
        view
        returns(uint256)
    {
        uint256 _teth = plyr_[_pAddress].curjoin;
        uint256 _rndrate;
        if(_probFixResW != 0)
            _rndrate = _probFixResW;
        else 
            _rndrate = getFixRetWRand(_pAddress);
        uint256 _income = _teth.mul(_rndrate).mul(_day).div(10000);
        return _canIncome < _income ? _canIncome : _income;
    }
```
* Calculate the expected return and the actual earned income based on the current latest participation, number of days, and income that can be received
