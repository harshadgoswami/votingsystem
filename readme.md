#command to combit sol file
.\node_modules\.bin\solcjs --bin --abi .\voting.sol

# all manual node js steps 
Execute this in your node console:
> bytecode = fs.readFileSync('./Voting_sol_Voting.bin').toString()
> abi = JSON.parse(fs.readFileSync('./Voting_sol_Voting.abi').toString())
> Web3 = require('web3')
> web3 = new Web3("http://localhost:8545")
> deployedContract = new web3.eth.Contract(abi)
> web3.eth.getAccounts(console.log) <- Should output 10 accounts
> listOfCandidates = ['Rama', 'Nick', 'Jose']
> deployedContract.deploy({
data: bytecode,
arguments: [listOfCandidates.map(name => web3.utils.asciiToHex(name))]
}).send({
from: 'ENTER YOUR ACCOUNT ADDRESS',
gas: 1500000,
gasPrice: web3.utils.toWei('0.00003', 'ether')
}).then((newContractInstance) => {
deployedContract.options.address = newContractInstance.options.address
console.log(newContractInstance.options.address) // instance with the new contract address
});

# mores
In your node console:
> deployedContract.methods

> deployedContract.methods.totalVotesFor(web3.utils.asciiToHex('Rama')).call(console.log)

> deployedContract.methods.voteForCandidate(web3.utils.asciiToHex('Rama')).send({from: 'YOUR ACCOUNT ADDRESS'}).then((f) => console.log(f))


