# provide/inject

Vue中provide/inject的值**不是响应式的**，如果想做成响应式，可以通过对数据进行包装：

* vue2：使用Vue.observable()
* vue3：使用ref/reactive，演示[入口](https://sfc.vuejs.org/#eNrNVM2O0zAQfpUhl+xKTczusaQViCsgJK6+pInbuiS2ZTtlUZUDEoc9gMQNceEN9gpC+zqUvgbj2O1uiroUcVkph/H8fPE3841X0ROl0mXDomGUmUJzZcEw26gxFbxWUltYgdJyyUs2AM2m0MJUyxpirIl3Oc95GdwpQdsBYpCKQgpjoZJFbrkUMHIIJ/ELLJnDS1mx+NRlUTFtRNFlNKrMLXsWCk4Mt+wUVlTADiRd5lXDEMrFqGhdebjgSbxNigf9ooE79LGxFH+eEU8a6eLBslpVmIMngKzkSyiq3JgRjXKlaNS5qc3mZ+PN5ffN9fuf199gtbrh17YZwWBImzTWovNxUfHiNWLsceu3IRqvP3z+9fVdRnzZsSCvZNMD+bgPQi2i4EyIJ0WQFVoZucU1M/Zt5UmnSLTrHMBE6pLpIZypCzCywgnPNGPikY+qvCy5mGH4obrofDgJ7GaHFA0iL4ykzlW6MFKgvDpYGgKGRkM/IudDubgzjebWKjMkxEwLp6GFSaWeEbRS3QjLa5YyUycTLd8YphGYRt1kAwZB55LpRDOBN2f6Lsy91D9wA6MWqTyV9W5FHiQJcIHfghVWaigwJgUTFpKk6+SBFfIFe8vjt+NGP4M9iWL6KFTekvY/qBZvF1SLgfn5eH31ZX316ZBwz++XcP+uVaT3/1qlAkcc3qzDj6DTwO6F2woCR3jsJGpe9ibhLYDN5Q8/jhDaTgFN95c7lrbfCsQ/2ArNyqOWtv0N4rMl+w==)



参见：

* [https://v2.vuejs.org/v2/api/?#provide-inject](https://v2.vuejs.org/v2/api/?#provide-inject)
* [https://vuejs.org/guide/components/provide-inject.html](https://vuejs.org/guide/components/provide-inject.html)
