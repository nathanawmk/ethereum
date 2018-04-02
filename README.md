# ethereum

https://ethereum.stackexchange.com/questions/44539/smart-contract-calling-an-external-api/44541#44541

pragma solidity ^0.4.16;
import "./usingOraclize.sol";  //Importing Oraclize
contract TestOraclizeCall is usingOraclize {
        uint public price;
       event Log(string text);
       //Constructor
       function TestOraclizeCall() {
             OAR = OraclizeAddrResolverI(0x5049063e4a7704ac155e4f1f42a4954bbef5bbde);
        }
  function __callback(bytes32 _myid, string _result) {
             require (msg.sender == oraclize_cbAddress());
             Log(_result);
              price = parseInt(_result, 2);
    }
    function update() payable {
            oraclize_query("URL","json(https://min-api.cryptocompare.com/data/price?fsym=ETH&tsyms=USD).USD");
    }
