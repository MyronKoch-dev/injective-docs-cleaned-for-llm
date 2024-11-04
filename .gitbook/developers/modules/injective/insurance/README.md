# Insurance

## Abstract

This paper specifies the insurance module of the Injective Chain.

This module provides insurance funds for derivative markets in the `exchange` module of the Injective Chain to use in order to support higher leverage trading. On a high level, insurance funds for each derivative market are funded by a permissionless group of underwriters, who each own a proportional claim (represented through insurance fund share tokens) over the underlying assets in the insurance fund.

Each insurance fund grows when positions in its corresponding derivative market are liquidated with positive equity, as half of the positive equity is sent to the insurance fund upon liquidation. When a position with negative equity is liquidated (i.e., the position has surpassed bankruptcy), the insurance fund is utilized to cover the missing equity.

## Contents

1. [**State**](https://github.com/InjectiveLabs/injective-docs/blob/gitbook/.gitbook/developers/modules/injective/insurance/01\_state.md)
2. [**State Transitions**](https://github.com/InjectiveLabs/injective-docs/blob/gitbook/.gitbook/developers/modules/injective/insurance/02\_state\_transitions.md)
3. [**Messages**](https://github.com/InjectiveLabs/injective-docs/blob/gitbook/.gitbook/developers/modules/injective/insurance/03\_messages.md)
4. [**End Block**](https://github.com/InjectiveLabs/injective-docs/blob/gitbook/.gitbook/developers/modules/injective/insurance/04\_end\_block.md)
5. [**Events**](https://github.com/InjectiveLabs/injective-docs/blob/gitbook/.gitbook/developers/modules/injective/insurance/05\_events.md)
6. [**Params**](https://github.com/InjectiveLabs/injective-docs/blob/gitbook/.gitbook/developers/modules/injective/insurance/06\_params.md)
7. [**Future Improvements**](https://github.com/InjectiveLabs/injective-docs/blob/gitbook/.gitbook/developers/modules/injective/insurance/07\_future\_improvements.md)