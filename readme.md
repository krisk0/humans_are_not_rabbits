# Humans are not Rabbits

Decrease bithrate, so most couples cannot have one child in one year.

## Technical requirements

Crusader Kings version 1.18.*

## Languages supported

English

## Motivation

I tweak birthrate parameters by installing mod [Elder Kings fixes and tweaks](https://github.com/krisk0/ek_fixes_and_tweaks). As a result, most landed characters that successfully defend their realm have dozens of childrens, approximately one baby per 16 months. The rate is even greater if culture/religion/dynasty gives bonus to fertility. This is unrealistic and makes game difficult to play.

To bring back some realism, I created this mod.

## How it works

With default base game setting NChildbirth::CHILD_BIRTH_TO_PREGNANCY_WAIT=3, there is three month cooldown after childbirth. After this cooldown is over, woman can theoretically get pregnant again. The setting is unchanged by [Elder Kings fixes and tweaks](https://github.com/krisk0/ek_fixes_and_tweaks).

This mod (Humans are not Rabbits) adds on childbirth two temporary modifiers to mother that decrease fertility. So women are less likely to get pregnant in 12 month again.

First debuff expires in two months after three month cooldown mentioned above. So most young women have nonzero chance to get pregnant in 14 month again. Second debuff expires in 7 months after first, fully restoring fertility.

## Theory and exact math

Crusader Kings 3 game engine keeps hidden modifier that applies to a married woman and on childbirth decreases her fertility for the purpose of calculating regular per-month pregnancy (default NChildbirth::MOTHER_FERTILITY_REDUCTION_PER_PREVIOUS_CHILD=0.05). Events that might result in pregnancy do not take this malus into account. If you install a mod that shows fertility, it would show event fertility, not marriage fertility. The marriage fertility is unavailable to CK3 scripts.

I decided to turn off the married woman debuf, so event fertility equals marriage fertility: `NChildbirth::MOTHER_FERTILITY_REDUCTION_PER_PREVIOUS_CHILD=0.0`.

With this and other tweaks from [Elder Kings fixes and tweaks](https://github.com/krisk0/ek_fixes_and_tweaks), married landowners with average fertility (0.5 for both spouses) have one baby per 16.5 month on average, if both spouses have no debuffs to fertility. The childbirth rate is even bigger if they have a personal/religious/cultural/dynastical bonus.

Consider example. A man with 60% fertility is married to a woman with 47% fertility, one of them is landowner,  [Elder Kings fixes and tweaks](https://github.com/krisk0/ek_fixes_and_tweaks) installed.
3 month after first baby was born, second baby will be conceived with percent chance `(0.6 + 0.47) / 2 * 50 = 26.7`. Which means second baby will be conceived in less than 4 month on average, so childbirth rate is slightly bigger than 1 baby per 16 month. Suppose mother and father are married at age 16. Then by age of 30 they will make more than 10 chilren on average. So they have a good chance to have twenty or more children in this marriage.

With this mod installed, mother will have negative fertility in 5 month after childbirth, because first malus lasts 5 month and decreases ferility by 40%, and second malus lasts one year and further decreases fertility by 20%. So 12 and 13 month after conceiving first baby, pregnancy is impossible. 14 month after conceiving first baby, mother's fertility will be 27%, which makes impregnation chance `(0.6 + 0.27) / 2 * 50 = 21.8`. So second baby will be conceived in approximately `14 + 5 = 19` months.

Thus, for this couple bithrate dropped from 1 baby per 16 month to 1 baby per 19 month after installation of the mod. The two numbers 1/16 and 1/19 are approximate. I want to give a general idea, not caculate the exact birthrate.

## My mods

List of my modifications for CK3, and my load order is [here](https://gist.github.com/krisk0/3c51136a877afd606c184a575400922f).
