# Sample Hardhat Project

This project demonstrates a basic Hardhat use case. It comes with a sample contract, a test for that contract, and a Hardhat Ignition module that deploys that contract.

Try running some of the following tasks:

```shell
npx hardhat help
npx hardhat test
REPORT_GAS=true npx hardhat test
npx hardhat node
npx hardhat ignition deploy ./ignition/modules/Lock.ts
```

---

#   Create dApp-nft blockchain use hardhat
1.  Khởi tạo dự án Hardhat với TypeScript
Chạy lệnh:
```shell
npx hardhat
```
-   Chọn tạo dự án TypeScript.

-   Hardhat tự tạo các thư mục và file mẫu (contracts/, scripts/, test/, hardhat.config.ts, ...).

2. Viết hợp đồng thông minh (smart contract)
-   Viết contract Solidity (ví dụ contracts/MyNFT.sol).

-   Mặc định có một contract mẫu trong thư mục contracts/.

3. Biên dịch (compile) contract
-   Chạy:
```shell
npx hardhat compile
```
-   Hardhat tải trình biên dịch Solidity về và tạo ra các file build trong artifacts/ và typechain-types/.

4. Chạy node local của Hardhat
-   Khởi động blockchain local để test:
```shell
npx hardhat node
```
-   Node này sẽ tạo ra 20 tài khoản test với ETH giả (chỉ chạy local).

5. Viết script deploy contract (TypeScript)
-   Trong thư mục scripts/ tạo file deploy.ts ví dụ:

```ts
import { ethers } from "hardhat";

async function main() {
    const [deployer] = await ethers.getSigners();
    console.log("Deploying contracts with the account:", deployer.address);

    const Contract = await ethers.getContractFactory("MyContract");
    const contract = await Contract.deploy();

    await contract.waitForDeployment();

    console.log("✅ Contract deployed to:", await contract.getAddress());
}

main().catch((error) => {
    console.error(error);
    process.exitCode = 1;
});
```
6. Triển khai (deploy) contract lên node local
Chạy:
```shell
npx hardhat run scripts/deploy.ts --network localhost
```
-   Contract được deploy, Hardhat in ra địa chỉ contract.

7. Kết nối và tương tác
-   Node local Hardhat đang chạy ở http://127.0.0.1:8545/.

-   Lưu ý: Truy cập trực tiếp địa chỉ này trên trình duyệt sẽ lỗi vì nó là API JSON-RPC.

-   Dùng thư viện ethers.js hoặc web3.js để kết nối và gọi contract.