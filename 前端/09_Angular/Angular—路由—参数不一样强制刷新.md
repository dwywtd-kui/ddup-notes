```typescript
this.router.navigateByUrl('', {skipLocationChange: true}).then(() => {
    this.router.navigate([url + '/' + id, {tabIndex: 1}]);
});
```
