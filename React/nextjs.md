# Nextjs

## App directory
### Directory naming tips
- `page.tsx`: this will be the index file for any page inside a directory.
- `some-folder/page.tsx` will mean you can visit `www.mysite.com/some-folder` and see the contents of `page.tsx`
- `(some-folder)` Parenthesis is purely for organization. The layout file in the parent folder will apply.
- `[id]` use brackets for dynamic pages. You can now visit `mysite.com/abcde`
- `[...id]` use three dots to indicate there may be any number of nested folders. You can now visit `mysite.com/myid/some-subsecton/sub-sub-sub`
- `[[...id]]` same as above, but you can also visit plane `mysite.com/abcde` without any sub-folders

