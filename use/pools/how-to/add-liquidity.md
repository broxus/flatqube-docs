# Add liquidity

Please note that this section assumes that you have already provided liquidity to the required pool. Otherwise, the process will be different - go to the [**new position page**](create-new-position.md).

## Simple liquidity provision

To add tokens to an existing position, go to the [Pools section](../), go to the [page of the desired pool](../interface/pool-page/) by clicking on the appropriate pair and click <mark style="color:red;">**Add Liquidity**</mark>.

After that, you will be taken to the page for adding liquidity to the pool.

![](<../../../.gitbook/assets/image (175).png>)

On this page, you can add a liquidation to the pool of this pair. \
\
Recall that you do not need to have both tokens in equal proportion on your balance, since FlatQube has an automatic exchange function, which also allows you to provide [**one-sided liqudity**](add-liquidity.md#one-sided-liquidity-provision).&#x20;

#### Adding liquidity on the example of the WEVER/USDC pair

To get started, enter the amount of tokens you wish to **add to the pool**. \
You can enter the amount of both the left and right token, and the required amount of the second token will be calculated automatically at the current FlatQube rate.

![](<../../../.gitbook/assets/image (52).png>)

After entering the amount, you will see how much your [**Pool share**](../pool-economics.md) will change, as well as the ratio of the price of tokens.

Now you need to consistently deposit tokens. Click Deposit and confirm the transaction in EVER Wallet.

![](<../../../.gitbook/assets/image (206).png>)

After a successful deposit of the left token, do the same for the right one:

![](<../../../.gitbook/assets/image (58).png>)

And here we are almost at the finish line - now it is necessary to produce **Supply**. \
This operation will also require confirmation.

![](<../../../.gitbook/assets/image (125).png>)

After the successful completion of the Supply, you will see **Supply receipt window.**

Here you will see the current **Pool share** and the percentage by which it was increased by this transaction, as well as the number of received [**LP tokens.**](calculate-the-amount-of-lp-tokens.md)****

![](<../../../.gitbook/assets/image (122).png>)

## One-sided liquidity provision

FlatQube has an automatic exchange feature that also allows you to provide one-way liquidity.

In order to provide liquidity using only one of the tokens, enable **Auto Exchange** and enter the amount of one of the tokens.

![](<../../../.gitbook/assets/image (102).png>)

Further actions are identical to the [**first example**](add-liquidity.md#adding-liquidity-on-the-example-of-the-wever-usdc-pair), with the difference that after depositing the token, we will immediately go to **Supply**.

![](<../../../.gitbook/assets/image (91).png>)

After the successful completion of the Supply, you will see **Supply receipt window.**

Here you will see the current **Pool share** and the percentage by which it was increased by this transaction, as well as the number of received [**LP tokens.**](calculate-the-amount-of-lp-tokens.md)****

![](<../../../.gitbook/assets/image (57).png>)
