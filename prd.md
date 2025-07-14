# TheAmericanSchema v0 - Simple PRD

## What This Is
A simple website that shows U.S. deportation numbers from official government data. No spin, no percentages, just the actual numbers with presidents' names above their terms.

## The One Chart That Matters
- **Type**: Line or area chart
- **X-axis**: Years (2009-2022)
- **Y-axis**: Number of people removed
- **Data**: From DHS Table 39 (Removals only)
- **Presidents**: Names/faces shown above their terms
- **Note**: "Showing formal removals only. Returns and expulsions excluded."

### Presidential Terms
```
Obama: 2009-2017
Trump: 2017-2021
Biden: 2021-2025
Trump: 2025-present
```

## Data Schemas

### Main Data File: `/src/data/deportations.json`
```typescript
interface DeportationData {
  source: DataSource;
  data: YearlyRemoval[];
}

interface DataSource {
  name: string;           // "DHS Yearbook of Immigration Statistics 2022"
  table: string;          // "Table 39"
  url: string;            // Link to official source
  extractedDate: string;  // ISO date when we extracted
  notes: string;          // "Removals only, excluding returns and expulsions"
}

interface YearlyRemoval {
  year: number;
  removals: number;
  president: "Obama" | "Trump" | "Biden";
}
```

### Future: Population Estimates (Phase 2)
```typescript
interface PopulationEstimates {
  sources: {
    [sourceName: string]: PopulationData[];
  };
}

interface PopulationData {
  year: number;
  estimate: number;
  notes?: string;
}

// Example:
{
  "sources": {
    "pew": [
      {"year": 2010, "estimate": 11200000},
      {"year": 2014, "estimate": 11300000}
    ],
    "dhs": [
      {"year": 2010, "estimate": 11600000}
    ]
  }
}
```

## Tech Stack (Dead Simple)
- **Framework**: React + Vite + TypeScript
- **Charts**: Recharts (simplest option)
- **Styling**: Tailwind CSS
- **Hosting**: Netlify (free)
- **Data**: Static JSON files

## File Structure
```
/src
  /data
    - deportations.json
    - population-estimates.json (future)
  /types
    - schemas.ts
  App.tsx (the chart)
  main.tsx
index.html
```

## The Entire App Flow
1. Load the page
2. See the chart with removals by year
3. Presidents clearly marked above their terms
4. Hover/tap for exact numbers
5. Source link at bottom
6. Note about excluding returns

## MVP Features (Day 1)
- [ ] One chart showing removals only
- [ ] Presidents labeled above their terms
- [ ] Source citation with link
- [ ] Note about what's excluded
- [ ] Mobile responsive
- [ ] Dark theme

## Phase 2 Features
- [ ] Population estimate selector
- [ ] Removal rate calculation (removals per 100k undocumented)
- [ ] Show uncertainty ranges

## Not in v0
- ❌ Returns data
- ❌ Expulsions data
- ❌ Multiple pages
- ❌ Complex interactions
- ❌ State-level data

## Success Criteria
- Shows accurate removal numbers from Table 39
- Clear about what's included/excluded
- Presidents clearly marked
- Works on phones
- Can be shared on social media

## Your TODO
1. ✅ Extract Table 39 data
2. Use the prompt above to have Claude parse it
3. Save as `/src/data/deportations.json`
4. Start gathering population estimates for Phase 2# TheAmericanSchema v0 - Simple PRD

## What This Is
A simple website that shows U.S. deportation numbers from official government data. No spin, no percentages, just the actual numbers with presidents' names above their terms.

## The One Chart That Matters
- **Type**: Line or area chart
- **X-axis**: Years (2009-2022, or whatever range you provide)
- **Y-axis**: Number of people
- **Data**: From DHS Table 39
- **Presidents**: Names/faces shown above their terms

### Presidential Terms
```
Obama: 2009-2017
Trump: 2017-2021
Biden: 2021-2025
Trump: 2025-present
```

## Data We Have
**Source**: DHS Yearbook 2022, Table 39
- Removals
- Administrative Returns
- Enforcement Returns  
- Expulsions

**Years**: You decide the range (suggestion: 2000-2022 or 2009-2022)

## Tech Stack (Dead Simple)
- **Framework**: React + Vite
- **Charts**: Recharts (simplest option)
- **Styling**: Tailwind CSS
- **Hosting**: Netlify (free)
- **Data**: One JSON file

## File Structure
```
/src
  /data
    - deportations.json
  App.tsx (the chart)
  main.tsx
index.html
```

## The Entire App Flow
1. Load the page
2. See the chart
3. Hover/tap for exact numbers
4. Source link at bottom
5. That's it

## Data Format
```json
{
  "source": "DHS Yearbook 2022, Table 39",
  "data": [
    {
      "year": 2009,
      "removals": 391953,
      "returns": 582596,
      "president": "Obama"
    },
    // ... more years
  ]
}
```

## MVP Features (Day 1)
- [ ] One chart showing the numbers
- [ ] Presidents labeled above their terms
- [ ] Source citation
- [ ] Mobile responsive
- [ ] Dark theme

## Not in v0
- ❌ Multiple data sources
- ❌ Comparison tools
- ❌ Factor analysis
- ❌ State-level data
- ❌ Complex interactions
- ❌ Multiple pages

## Success Criteria
- Shows accurate numbers from Table 39
- Works on phones
- Loads fast
- Can be shared on social media

## Your TODO
1. Extract Table 39 data for chosen years
2. Decide: Show all columns or just removals?
3. Provide CSV like:
   ```csv
   year,removals,returns,president
   2009,391953,582596,Obama
   ```

## Questions to Answer
1. Which years to show? (2009-2022? 2000-2022? 1990-2022?)
2. Combine returns or show separately?
3. Include expulsions?

That's it. One page, one chart, real numbers.