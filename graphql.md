```gql
query {
	continents {
		name
		countries {
			name
			continent {
				countries {
					name
					languages {
						name
                        native
					}
				}
			}
		}
	}
}
```