# GitHub action to add a label to Glo Boards cards

Use this action to add a label to cards on a [Glo Board](https://www.gitkraken.com/glo).
The action requires an array of objects with board and card IDs, and the label name as inputs.

## Requirements
The action requires an auth token in the form of a PAT that you can create in your GitKraken account.
See the [Personal Access Tokens](https://support.gitkraken.com/developers/pats/) page on our support site.

This token should be stored in your GitHub repo secrets (in repo Settings -> Secrets).

## Inputs
The `cards` input is an array of objects that contain the board ID and card ID pairs:
```ts
interface ICard {
  boardId: string;
  cardId: string;
}
```

The `labelName` input is the name of a label that already exists in the Glo Board.

## Examples
Add a step in your workflow file to perform this action and use the output of the `glo-action-parse-links` action:
```yaml
    steps:
    - uses: Axosoft/glo-action-parse-links@v1
      id: glo-parse

    - uses: Axosoft/glo-action-label-card@v1
      with:
        authToken: ${{ secrets.GLO-PAT }}
        cards: '${{ steps.glo-parse.outputs.cards }}'
        label: 'Released'
      id: glo-label
```
