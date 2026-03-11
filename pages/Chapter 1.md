-
- query-table:: false
  #+BEGIN_QUERY
  {:title [:h2 "Draft Content"]
   :query [:find (pull ?c [*])
           :where
           [?p1 :block/name "chapter 1"]
           [?p2 :block/name "paragraph"]
           [?b :block/refs ?p1]
           [?b :block/refs ?p2]
           [?c :block/parent ?b]]
   :breadcrumb-show? false}
  #+END_QUERY
- My text is here and it is longer
- #+BEGIN_QUERY
  {:title "Draft Content"
   :query [:find (pull ?c [*])
           :where
           [?p1 :block/name "chapter 1"]
           [?p2 :block/name "paragraph"]
           [?b :block/refs ?p1]
           [?b :block/refs ?p2]
           [?c :block/parent ?b]]
   :breadcrumb-show? false}
  #+END_QUERY