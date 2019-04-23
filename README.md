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
	if(rand(100, _pAddress) < 50){
		inc_ = inc_ + 3;
	}else{
		inc_ = inc_ + 5;
	}
	return inc_;
}

```
* Random number generation
* Random seed acquisition
