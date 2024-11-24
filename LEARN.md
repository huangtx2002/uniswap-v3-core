V2: constant product formula - x*y=k
V3: concentrated liquidity market maker - L = delta(x) / delta(sqrt(price))
Impermanent Loss - IL = (2 * sqrt(Pfinal/Pinitial))/(1+Pfinal/Pinitial) - 1
price = (1.0001) \*\* tick

msg.sender - contract user
this - contract this

interfaces-callback
IUniswapV3FlashCallback.sol - Any contract that calls IUniswapV3PoolActions#flash must implemnt this interface

IUniswapV3MintCallback.sol - Any contract that calls IUniswapV3PoolActions#mint must implement this interface

IUniswapV3SwapCallback.sol - Any contract that calls IUniswapV3PoolActins#swap must implemnt this interface

interfaces-pool
IUniswapV3PoolActions.sol - contains pool methods that can be called by anyone - function initialize(uint160 sqrtPriceX96) external
sqrtPriceX96: sqrt(amountToken1/amountToken0) - function mint(address recipient,int24 tickLower, int24 tickUpper, uint128 amount, bytes calldata data) external returns(uint256 amount0, uint256 amouot1) - function collect(address recipient, int24 tickLower, int24 tickUpper, uint128 amount0Reqeusted, uint128 amount1Requested) external returns (uint128 amount0, uint128 amount1) - function burn(int24 tickLower, int24 tickUpper, uint128 amount) external returns(uint256 amount0, uint256 amount1) - function swap(address recipient, bool zeroForOne, int256 amountSpcified, uint160 sqrtPriceLimitX96, bytes calldata data) external returns (int256 amount0, int256 amount1) - function flash(address recipient, uint256 amount0, uint256 amount1, bytes calldata data) external -

IUniswapV3PoolDerivedState.sol - Contains view functions to provide information about the pool that is computed rather than stored on the blockchain. The functions here may have variable gas costs. - function observe(uint32[] calldata secondsAgos) external view returns (int56[] memory tickCumulatives, uint160[] memory secondsPerLiquidityCumulativeX128s) - function snapshotCumulativesInside(int24 tickLower, int24 tickUpper) external view returns (int56 tickCumulativeInside, uint160 secondsPerLiquidityInsideX128, uint32 secondsInside)

IUniswapV3PoolEvents.sol - Events emitted by a pool - event Initialize(uint160 sqrtPriceX96, int24 tick) - event Mint(address sender, address indexed owner, int24 indexed tickLower, int24 indexed tickUpper, uint128 amount, uint256 amount0, uint256 amount1) - event Collect(address indexed owner, address recipient, int24 indexed tickLower, int24 indexed tickUpper, uint128 amount0, uint128 amount1) - event Burn(address indexed owner, int24 indexed tickLower, int24 indexed tickUpper, uint128 amount, uint256 amount0, uint256 amount1) - event Swap(address indexed sender, address indexed recipient, int256 amount0, int256 amount1, uint160 sqrtPriceX96, uint128 liquidity, int24 tick) - event Flash(address indexed sender, address indexed recipient uint256 amount0, uint256 amount1, uint256 paid0, uint256 paid1) - event IncreaseObservationCardinalityNext( uint16 observationCardinalityNextOld, uint16 observationCardinalityNextNew) - event SetFeeProtocol(uint8 feeProtocol0Old, uint8 feeProtocol1Old, uint8 feeProtocol0New, uint8 feeProtocol1New) - event CollectProtocol(address indexed sender, address indexed recipient, uint128 amount0, uint128 amount1)

IUniswapV3PoolImmutables.sol - Pool state that never changes - function factory() external view returns (address) - function token0() external view returns (address) - function token1() external view returns (address) - function fee() external view returns (uint24) - function tickSpacing() external view returns (int24) - function maxLiquidityPerTick() external view returns (uint128)

IUniswapV3PoolOwnerActions.sol - Permissioned pool actions - function setFeeProtocol(uint8 feeProtocol0, uint8 feeProtocol1) external - function collectProtocol(address recipient, uint128 amount0Requested, uint128 amount1Requested) external returns (uint128 amount0, uint128 amount1)

IUniswapV3PoolState.sol - Pool state that can change - function slot0() external view returns (uint160 sqrtPriceX96, int24 tick, uint16 observationIndex, uint16 observationCardinality, uint16 observationCardinalityNext, uint8 feeProtocol, bool unlocked) - function feeGrowthGlobal0X128() external view returns (uint256) - function feeGrowthGlobal1X128() external view returns (uint256) - function protocolFees() external view returns (uint128 token0, uint128 token1) - function liquidity() external view returns (uint128) - function ticks(int24 tick) external view returns (uint128 liquidityGross, int128 liquidityNet, uint256 feeGrowthOutside0X128, uint256 feeGrowthOutside1X128, int56 tickCumulativeOutside, uint160 secondsPerLiquidityOutsideX128, uint32 secondsOutside, bool initialized)

intefaces
IERC20Minimal.sol - Minimal ERC20 interface for Uniswap - function balanceOf(address account) external view returns (uint256) - function transfer(address recipient, uint256 amount) external returns (bool) - function allowance(address owner, address spender) external view returns (uint256) - function approve(address spender, uint256 amount) external returns (bool) - function transferFrom(address sender, address recipient, uint256 amount) external returns (bool) - event Transfer(address indexed from, address indexed to, uint256 value) - event Approval(address indexed owner, address indexed spender, uint256 value)

IUniswapV3Factory.sol - The interface for the Uniswap V3 Factory - event OwnerChanged(address indexed oldOwner, address indexed newOwner) - event PoolCreated(address indexed token0, address indexed token1, uint24 indexed fee, int24 tickSpacing, address pool) - event FeeAmountEnabled(uint24 indexed fee, int24 indexed tickSpacing) - function owner() external view returns (address) - function feeAmountTickSpacing(uint24 fee) external view returns (int24) - function getPool(address tokenA, address tokenB, uint24 fee ) external view returns (address pool) - function createPool(address tokenA, address tokenB, uint24 fee ) external returns (address pool) - function setOwner(address \_owner) external - function enableFeeAmount(uint24 fee, int24 tickSpacing) external

IUniswapV3Pool.sol - The interface for a Uniswap V3 Pool - interface IUniswapV3Pool is IUniswapV3PoolImmutables,
IUniswapV3PoolState, IUniswapV3PoolDerivedState, IUniswapV3PoolActions, IUniswapV3PoolOwnerActions, IUniswapV3PoolEvents {}

IUniswapV3PoolDeployer.sol - An interface for a contract that is capable of deploying Uniswap V3 Pools -
function parameters() external view returns (address factory, address token0, address token1, uint24 fee, int24 tickSpacing)
