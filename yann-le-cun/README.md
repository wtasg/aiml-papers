# Yann Le Cun

## Download Papers

1. Go to [arxiv search page 1-200](https://arxiv.org/search/?searchtype=author&query=LeCun%2C+Y&abstracts=show&size=200&order=-announced_date_first)
2. Execute `console.log(Array.from(document.querySelectorAll('a[href^="https://arxiv.org/pdf/"]')).map(a => a.href).join("\n"));`
3. Copy and Paste text to a text file
4. Go to [arxiv search page 200+](https://arxiv.org/search/?searchtype=author&query=LeCun%2C+Y&abstracts=show&size=200&order=-announced_date_first&start=200)
5. Repeat 2 and 3
6. Execute following bash script

```bash
for file in `cat /home/user/notes/scratches/data/yann-le-cun-papers.txt`
do
    echo "$file";
    curl -O "$file";
done
```
