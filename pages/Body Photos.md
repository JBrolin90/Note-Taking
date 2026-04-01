tags:: #Health #[[Logseq Query]]

- #+BEGIN_QUERY
  {:query
  [:find (pull ?b [*])
     :where
        [page-ref ?b "photos"  ]
        [page-ref ?b "morning"  ]
        [page-ref ?b "health"  ]
  ]
  }
  #+END_QUERY
-